# Firebase Lecture 01

> # Firebase Auth - Sign In

```
Future SignIn() async {
    await FirebaseAuth.instance.signInWithEmailAndPassword(
        email : emailController.text.trim(),
        password : passwordController.text.trim(),
    );
}
```

>Main Page
```
class MyApp extends statelessWidget {
    @override
    Widget build(BuildContext context) => Scaffold(
        body: StreamBuilder<User?>(
            stream: FirebaseAuth.instance.authChanges(),
            builder: (context , snapshot) {
                if(snapshot.hasData) {
                    return HomePage();
                }
                else {
                    return LoginWidget();
                }
            }
        ),
    );
}
```

> # Firebase Auth - Sign Up

```
TextFormField(
    controller: passwordController,
    textInputAction: TextInputAction.next,
    decoration: InputDecoration(labelText: 'Password'),
    obsecuredText: true,
    autoValidateMode: AutoValidate.onUserInteraction,
    validator: (value) => value != null && value.length < 6 
    ? 'Enter min 6 characters'
    : null,
)
```

```
Future SignUp() async {
    final isValid = formKey.currentState!.validate();
    if (!isValid) return;

    showDialog(
      context: context,
      barrierDismissible: false,
      builder: (context) => Center(child: CircularProgressIndicator()),
    );

    try {
      await FirebaseAuth.instance.createUserWithEmailAndPassword(
        email: emailController.text.trim(),
        password: passwordController.text.trim(),
      );
    } on FirebaseAuthException catch (e) {
      print(e);

    final snackBar = SnackBar(content: e.message.toString , backgroundColor: Colors.red);


    ScaffoldMessenger.of(context).showSnackBar(snackbar);

    }

    navigatorKey.currentState!.popUntil((route) => route.isFirst);
  }
}
```


> # Firebase Auth - Forgot password

```
Future resetPassword () async {

  showDialog(
      context: context,
      barrierDismissible: false,
      builder: (context) => Center(child: CircularProgressIndicator()),
    );

    try {
    await FirebaseAuth.instance
        .sendPasswordResetEmail(email: emailController.trim());

    final snackBar = SnackBar(content:'Email has been send' , backgroundColor: Colors.red);

    ScaffoldMessage.of(context).showSnackBar(snackbar);
    } on FirebaseAuthException catch(e) {
      print(e);

      final snackBar = SnackBar(content: e.message.toString , backgroundColor: Colors.red);


    ScaffoldMessenger.of(context).showSnackBar(snackbar);
    Navigator.of(context).pop();
    }
}
```
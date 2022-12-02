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
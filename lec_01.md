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
final signUp() async{
    final isValid = formKey.currentState!.validate();

    if(!isValid) return;
}
```

>utils.dart

```
import 'package:flutter/material.dart';

final messengerKey = GlobalKey<ScaffoldMessengerState>();

class Utils {
    static showSnackBar(String? text) {
        if(text == null) return;

        final snackBar = SnackBar(content: Text(text),backgroundColor : Colors.red);

        messengerKey.currentState!
        ..removeCurrentSnackBar()
        ..showSnackBar(snackbar);
    }
}
```
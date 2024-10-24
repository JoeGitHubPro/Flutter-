


Project Structure:


simple_api_example
  /lib
    /models
      post_model.dart
    /services
      api_service.dart
    /screens
      home_page.dart
    main.dart
  pubspec.yaml



### Step 1: pubspec.yaml

This file manages dependencies. Add the http package.
yaml
```yaml
name: simple_api_example
description: A simple Flutter app that calls an API.

version: 1.0.0+1

environment:
  sdk: ">=2.17.6 <3.0.0"

dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.4

dev_dependencies:
  flutter_test:
    sdk: flutter

flutter:
  uses-material-design: true

```


 ---
### Step 2: lib/models/post_model.dart

#### This file defines the data model for the API response.



```dart
class Post {
  final string profiel_image_link;
  final String title;
  final String body;

  Post({required this.profiel_image_link, required this.title, required this.body});

  factory Post.fromJson(Map<String, dynamic> json) {
    return Post(
      id: json['profiel_image_link'],
      title: json['title'],
      body: json['body'],
    );
  }
}

```


---
### Step 3: lib/services/api_service.dart

#### This file handles the API call.

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
import '../models/post_model.dart';

class ApiService {
  Future<Post?> fetchPost() async {
    final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));

    if (response.statusCode == 200) {
      return Post.fromJson(jsonDecode(response.body));
    } else {
      throw Exception('Failed to load post');
    }
  }
}

```


### Step 4: lib/screens/home_page.dart

#### This is the UI of the app that displays the data.
```dart
import 'package:flutter/material.dart';
import '../models/post_model.dart';
import '../services/api_service.dart';

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  late Future<Post?> post;

  @override
  void initState() {
    super.initState();
    post = ApiService().fetchPost();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Simple API Example'),
      ),
      body: Center(
        child: FutureBuilder<Post?>(
          future: post,
          builder: (context, snapshot) {
            if (snapshot.connectionState == ConnectionState.waiting) {
              return CircularProgressIndicator();
            } else if (snapshot.hasError) {
              return Text('Error: ${snapshot.error}');
            } else if (snapshot.hasData) {
              return Padding(
                padding: const EdgeInsets.all(16.0),
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    Text('Title: ${snapshot.data?.title ?? 'No data'}',
                        style: TextStyle(fontSize: 24)),
                    SizedBox(height: 20),
                    Text('Body: ${snapshot.data?.body ?? 'No data'}',
                        style: TextStyle(fontSize: 16)),
                  ],
                ),
              );
            } else {
              return Text('No data available');
            }
          },
        ),
      ),
    );
  }
}

```


---
### Step 5: lib/main.dart

#### The main entry point for the app.
```dart
import 'package:flutter/material.dart';
import 'screens/home_page.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Simple API Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomePage(),
    );
  }
}

```


---

##### Explanation:

###### 1. Model (post_model.dart): Defines the structure of the Post object to map the API response.


###### 2. Service (api_service.dart): Contains the function that hand…

###### 3. Screen (home_page.dart): The user interface of the app. It uses FutureBuilder to asynchronously wait for the API data and display it when available.


###### 4. Main (main.dart): Starts the app and sets the initial home screen.



How It Works:

When the app is opened, the HomePage widget makes a GET request using ApiService. The data is fetched and displayed using a FutureBuilder widget that handles loading, success, and error states.


This is a modularized version of the API call in Flutter.


# Roadmap : 

##### Flutter crash course : 

https://www.youtube.com/watch?v=6bSP4vazmyw&list=PL93xoMrxRJIvtIXjAiX15wcyNv-LOWZa9
  ---

##### Flutter Provider state management :   
[https://www.youtube.com/watch?v=3Yj45F5_a8o&list=PL93xoMrxRJIviJiC76oO5aV8bDp2s3OrA](https://www.youtube.com/watch?v=3Yj45F5_a8o&list=PL93xoMrxRJIviJiC76oO5aV8bDp2s3OrA)
 
 ---
  
 
##### flutter bloc state managment:
[https://www.youtube.com/watch?v=1BR3oa9bwLM&list=PLwWuxCLlF_ufA0GYYjlx_R4smekKH_AuB](https://www.youtube.com/watch?v=1BR3oa9bwLM&list=PLwWuxCLlF_ufA0GYYjlx_R4smekKH_AuB)

---
##### flutter Api :
[https://www.youtube.com/watch?v=IQ6NJ8JoO9E&list=PL3aG1K3LWCre6DIC2amKlXjn_kd2P6zE9](https://www.youtube.com/watch?v=IQ6NJ8JoO9E&list=PL3aG1K3LWCre6DIC2amKlXjn_kd2P6zE9)







# shorts:

#####  Stateless vs. Stateful - Flutter :

 [https://www.youtube.com/watch?v=pvEfXKifO4U&pp=ygUec3RhdGVmdWwgdnMgc3RhdGVsZXNzIGZsdXR0ZXIg](https://www.youtube.com/watch?v=pvEfXKifO4U&pp=ygUec3RhdGVmdWwgdnMgc3RhdGVsZXNzIGZsdXR0ZXIg)

---
#####  Comparing Between Provider, Bloc and GetX in Flutter with Example :

 [https://www.youtube.com/watch?v=lg_Fl7adAVY&pp=ygUYZ2V0eCB2cyBwcm92aWRlciB2cyBibG9j](https://www.youtube.com/watch?v=lg_Fl7adAVY&pp=ygUYZ2V0eCB2cyBwcm92aWRlciB2cyBibG9j)

---


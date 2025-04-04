# Settarplay
"Settar play - aplikasi hiburan all-in-on terbaik"
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'package:firebase_auth/firebase_auth.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
import 'package:firebase_storage/firebase_storage.dart';
import 'package:video_player/video_player.dart';
import 'package:image_picker/image_picker.dart';
import 'package:flutter_chat_ui/flutter_chat_ui.dart';
import 'package:flutter_chat_types/flutter_chat_types.dart' as types;
import 'package:audioplayers/audioplayers.dart';
import 'package:provider/provider.dart';
import 'package:livekit_client/livekit_client.dart';
import 'dart:io';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(SettarPlayApp());
}

class SettarPlayApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (_) => AuthProvider()),
      ],
      child: MaterialApp(
        title: 'Settar Play',
        theme: ThemeData.dark(),
        home: HomePage(),
      ),
    );
  }
}

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Settar Play')),
      body: Center(
        child: SingleChildScrollView(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text('Welcome to Settar Play!'),
              SizedBox(height: 20),
              ElevatedButton(
                onPressed: () => Navigator.push(context, MaterialPageRoute(builder: (_) => LoginPage())),
                child: Text('Login'),
              ),
              ElevatedButton(
                onPressed: () => Navigator.push(context, MaterialPageRoute(builder: (_) => RegisterPage())),
                child: Text('Register'),
              ),
              ElevatedButton(
                onPressed: () => Navigator.push(context, MaterialPageRoute(builder: (_) => VideoUploadPage())),
                child: Text('Upload Video'),
              ),
              ElevatedButton(
                onPressed: () => Navigator.push(context, MaterialPageRoute(builder: (_) => ShopPage())),
                child: Text('Shop'),
              ),
              ElevatedButton(
                onPressed: () => Navigator.push(context, MaterialPageRoute(builder: (_) => ChatPage())),
                child: Text('Live Chat'),
              ),
              ElevatedButton(
                onPressed: () => Navigator.push(context, MaterialPageRoute(builder: (_) => MusicPlayerPage())),
                child: Text('Play Music'),
              ),
              ElevatedButton(
                onPressed: () => Navigator.push(context, MaterialPageRoute(builder: (_) => LiveStreamPage())),
                child: Text('Live Streaming'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}

class LiveStreamPage extends StatefulWidget {
  @override
  _LiveStreamPageState createState() => _LiveStreamPageState();
}

class _LiveStreamPageState extends State<LiveStreamPage> {
  late Room room;
  
  @override
  void initState() {
    super.initState();
    _connectToRoom();
  }

  void _connectToRoom() async {
    room = Room();
    await room.connect('your-livekit-url', 'your-token');
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Live Streaming')),
      body: Center(child: Text('Live Streaming (Coming Soon)')),
    );
  }
}

class AuthProvider extends ChangeNotifier {
  User? user;

  void login(String email, String password) async {
    user = (await FirebaseAuth.instance.signInWithEmailAndPassword(email: email, password: password)).user;
    notifyListeners();
  }

  void register(String email, String password) async {
    u

# basic-weather-App
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:http/http.dart'as http;


void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: WeatherApp(),
    );
  }
}

class WeatherApp extends StatefulWidget {
  const WeatherApp({super.key});

  @override
  State<StatefulWidget> createState() {
    return Weatherscreenstate();
  }
}

class Weatherscreenstate extends State<WeatherApp> {


String Temperature='Temperature--';
String feelslike='feelslike--';
String windspreed='windspreed--';
String humidity='Humidity--';
String visibilty='Visibity--';
String pressure='Pressure';
String Icon='';
String city='';
String key="09c57e025b5c46f693a135832250505";














  TextEditingController cityController=TextEditingController();

   Future< void> Getdata() async{

      Uri url=Uri.parse("http://api.weatherapi.com/v1/current.json?key=$key&q=$city");


   final response= await http.get(url,headers: {"accept":"application/jason"});

   final body=json.decode(response.body);
   setState(() {
      Temperature='Temperature:${body["current"]["temp_c"]} Degree';
      feelslike='feelslike:${body["current"]["temp_f"]}Degree';
      windspreed='windspreed:${body["current"][ "wind_kph"]}kph';
      humidity='Humidity:${body["current"][ "humidity"]}';
      visibilty='Visibit:${body["current"][ "vis_km"]}km';
      pressure='Pressure:${body["current"][ "pressure_mb"]}mb';

   });
   }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Weatherdata'),
        centerTitle: true,
      ),
      body: Padding(
        padding: EdgeInsets.all(20),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TextField(
              controller: cityController ,
              decoration: InputDecoration(
                border: OutlineInputBorder(),
              ),
            ),
            SizedBox(
              height: 20,
            ),
            ElevatedButton(
              onPressed: () {
                setState(() {
                  city=cityController.text;
                });
                Getdata();

              },
              child: Text('Get data'),
            ),
            SizedBox(
              height: 40,
            ),
            Text(
              Temperature,
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.w900),
            ),

            Text(
              feelslike,
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.w900),
            ),
            Text(
                 windspreed,
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.w900),
            ),
            Text(
              humidity,
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.w900),
            ),
            Text(
              visibilty,
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.w900),
            ),
            Text(
              pressure,
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.w900),

            ),Text(
              city  ,
        style: TextStyle(fontSize: 20, fontWeight: FontWeight.w900),)

          ],
        ),
      ),
    );
  }
}

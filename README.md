# Mobile-programming-project
import 'package:flutter/material.dart';

void main() {
  runApp(const JyotirlingaApp());
}

class JyotirlingaApp extends StatelessWidget {
  const JyotirlingaApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'On the roots!',
      theme: ThemeData(primarySwatch: Colors.orange, fontFamily: 'Poppins'),
      home: const JyotirlingaHomePage(),
    );
  }
}

class JyotirlingaHomePage extends StatelessWidget {
  const JyotirlingaHomePage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Container(
        decoration: const BoxDecoration(
          gradient: LinearGradient(
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
            colors: [Color(0xFFFFA500), Color(0xFFFF4500)],
          ),
        ),
        child: SafeArea(
          child: Column(
            children: [
              const Padding(
                padding: EdgeInsets.all(16.0),
                child: Text(
                  'Sacred Jyotirlinga Yatra',
                  style: TextStyle(
                    fontSize: 28,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                    fontFamily: 'Devanagaric',
                  ),
                ),
              ),
              Expanded(
                child: ListView.builder(
                  padding: const EdgeInsets.all(16),
                  itemCount: jyotirlingaList.length,
                  itemBuilder: (context, index) {
                    final temple = jyotirlingaList[index];
                    return GestureDetector(
                      onTap:
                          () => Navigator.push(
                            context,
                            MaterialPageRoute(
                              builder:
                                  (context) => TempleDetailPage(temple: temple),
                            ),
                          ),
                      child: Card(
                        elevation: 5,
                        margin: const EdgeInsets.only(bottom: 16),
                        shape: RoundedRectangleBorder(
                          borderRadius: BorderRadius.circular(15),
                        ),
                        child: Column(
                          children: [
                            ClipRRect(
                              borderRadius: const BorderRadius.vertical(
                                top: Radius.circular(15),
                              ),
                              child: Image.network(
                                temple.imageUrl,
                                height: 200,
                                width: double.infinity,
                                fit: BoxFit.cover,
                              ),
                            ),
                            Padding(
                              padding: const EdgeInsets.all(16.0),
                              child: Column(
                                crossAxisAlignment: CrossAxisAlignment.start,
                                children: [
                                  Text(
                                    temple.name,
                                    style: const TextStyle(
                                      fontSize: 22,
                                      fontWeight: FontWeight.bold,
                                      color: Colors.orange,
                                    ),
                                  ),
                                  const SizedBox(height: 8),
                                  Text(
                                    temple.location,
                                    style: const TextStyle(
                                      fontSize: 16,
                                      color: Colors.grey,
                                    ),
                                  ),
                                  const SizedBox(height: 8),
                                  Text(
                                    'Package: ₹${temple.packagePrice}',
                                    style: const TextStyle(
                                      fontSize: 18,
                                      fontWeight: FontWeight.bold,
                                      color: Colors.green,
                                    ),
                                  ),
                                ],
                              ),
                            ),
                          ],
                        ),
                      ),
                    );
                  },
                ),
              ),
            ],
          ),
        ),
      ),
      floatingActionButton: FloatingActionButton.extended(
        onPressed: () {
          // Add booking functionality
        },
        label: const Text('Book Complete Yatra'),
        icon: const Icon(Icons.flight_takeoff),
      ),
    );
  }
}

class TempleDetailPage extends StatelessWidget {
  final Temple temple;

  const TempleDetailPage({Key? key, required this.temple}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: CustomScrollView(
        slivers: [
          SliverAppBar(
            expandedHeight: 300,
            pinned: true,
            flexibleSpace: FlexibleSpaceBar(
              title: Text(temple.name),
              background: Image.network(temple.imageUrl, fit: BoxFit.cover),
            ),
          ),
          SliverToBoxAdapter(
            child: Container(
              decoration: const BoxDecoration(
                gradient: LinearGradient(
                  colors: [Colors.orange, Colors.deepOrange],
                  begin: Alignment.topLeft,
                  end: Alignment.bottomRight,
                ),
              ),
              child: Padding(
                padding: const EdgeInsets.all(16.0),
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text(
                      'Location: ${temple.location}',
                      style: const TextStyle(
                        fontSize: 20,
                        color: Colors.white,
                        fontWeight: FontWeight.bold,
                      ),
                    ),
                    const SizedBox(height: 16),
                    Text(
                      temple.description,
                      style: const TextStyle(fontSize: 16, color: Colors.white),
                    ),
                    const SizedBox(height: 16),
                    Card(
                      child: Padding(
                        padding: const EdgeInsets.all(16.0),
                        child: Column(
                          crossAxisAlignment: CrossAxisAlignment.start,
                          children: [
                            const Text(
                              'Package Details',
                              style: TextStyle(
                                fontSize: 22,
                                fontWeight: FontWeight.bold,
                              ),
                            ),
                            const SizedBox(height: 8),
                            Text(
                              '• Package Price: ₹${temple.packagePrice}',
                              style: const TextStyle(fontSize: 18),
                            ),
                            const Text(
                              '• 2 Days & 1 Night',
                              style: TextStyle(fontSize: 18),
                            ),
                            const Text(
                              '• Hotel Accommodation',
                              style: TextStyle(fontSize: 18),
                            ),
                            const Text(
                              '• Temple Visit with Guide',
                              style: TextStyle(fontSize: 18),
                            ),
                          ],
                        ),
                      ),
                    ),
                    const SizedBox(height: 16),
                    SizedBox(
                      width: double.infinity,
                      child: ElevatedButton(
                        onPressed: () {
                          // Add booking functionality
                        },
                        style: ElevatedButton.styleFrom(
                          padding: const EdgeInsets.all(16),
                        ),
                        child: const Text(
                          'Book Now',
                          style: TextStyle(fontSize: 18),
                        ),
                      ),
                    ),
                  ],
                ),
              ),
            ),
          ),
        ],
      ),
    );
  }
}

class Temple {
  final String name;
  final String location;
  final String description;
  final String imageUrl;
  final int packagePrice;

  Temple({
    required this.name,
    required this.location,
    required this.description,
    required this.imageUrl,
    required this.packagePrice,
  });
}

final List<Temple> jyotirlingaList = [
  Temple(
    name: 'Somnath Temple',
    location: 'Gujarat',
    description:
        'The first among the twelve Jyotirlinga shrines of Shiva, Somnath Temple is located in Prabhas Patan, Gujarat. The temple is believed to have been built in gold by the moon god Soma.',
    imageUrl:
        'https://upload.wikimedia.org/wikipedia/commons/thumb/1/10/Somanath_mandir_%28cropped%29.jpg/1024px-Somanath_mandir_%28cropped%29.jpg',
    packagePrice: 12999,
  ),
  Temple(
    name: 'Mallikarjuna Temple',
    location: 'Andhra Pradesh',
    description:
        'Located on the Shrisailam hills in Andhra Pradesh, Mallikarjuna Temple is dedicated to both Lord Shiva and Goddess Parvati.',
    imageUrl:
        'https://1.bp.blogspot.com/-UXcznmt3MsM/UHGsP1q6LzI/AAAAAAAAH0A/TrePc2_u6jA/s1600/mallikarjuna2.jpg', // Replace with actual image URL
    packagePrice: 11999,
  ),
  Temple(
    name: 'Rameshwaram',
    location: 'Tamilnadu',
    description:
        'Rameshwaram Temple, a sacred Hindu shrine located on the island of Rameswaram, Tamil Nadu, India, is one of the four Char Dham pilgrimage sites and a revered destination for Lord Shiva devotees.',
    imageUrl:
        'https://upload.wikimedia.org/wikipedia/commons/thumb/8/84/Ramanathaswamy_temple7.JPG/800px-Ramanathaswamy_temple7.JPG',
    packagePrice: 15999,
  ),
  Temple(
    name: 'Kedarnath',
    location: 'Uttarakhand',
    description:
        'Kedarnath Temple, nestled in the majestic Himalayas, Uttarakhand, India, is a sacred Hindu shrine and one of the four Char Dham pilgrimage sites, revered for its stunning architecture and spiritual significance as the abode of Lord Shiva.',
    imageUrl:
        'https://upload.wikimedia.org/wikipedia/commons/thumb/5/56/Kedarnath_Temple_in_Rainy_season.jpg/1024px-Kedarnath_Temple_in_Rainy_season.jpg',
    packagePrice: 20000,
  ),
  Temple(
    name: 'Baidyanath',
    location: 'Uttarakhand',
    description:
        'Baidyanath Temple, situated in the picturesque Garhwal Himalayas, Uttarakhand, India, is a sacred Hindu pilgrimage site and one of the four Char Dham destinations, revered for its stunning natural beauty and spiritual significance as the abode of Lord Vishnu.',
    imageUrl:
        'https://upload.wikimedia.org/wikipedia/commons/thumb/f/f9/Badrinath_Temple_%2C_Uttarakhand.jpg/1024px-Badrinath_Temple_%2C_Uttarakhand.jpg',
    packagePrice: 19000,
  ),
  Temple(
    name: 'Kashi Vishwanath',
    location: 'Varanasi',
    description:
        'Kashi Vishwanath Temple, located on the banks of the Ganges River in Varanasi, India, is one of the twelve Jyotirlingas and a sacred Hindu shrine revered for its spiritual significance and historical importance as a revered abode of Lord Shiva.',
    imageUrl:
        'https://upload.wikimedia.org/wikipedia/commons/f/ff/Kashi_Vishwanath.jpg',
    packagePrice: 20999,
  ),
  Temple(
    name: 'Mahakaleshwar',
    location: 'Ujjain',
    description:
        'Mahakaleshwar Temple, located in Ujjain, Madhya Pradesh, India, is one of the twelve Jyotirlingas and a sacred Hindu shrine revered for its spiritual significance and historical importance as a revered abode of Lord Shiva, also known as Mahakal.',
    imageUrl:
        'https://upload.wikimedia.org/wikipedia/commons/thumb/7/7d/Mahakal_Temple_Ujjain.JPG/800px-Mahakal_Temple_Ujjain.JPG',
    packagePrice: 20999,
  ),
  Temple(
    name: 'Nageshwar',
    location: 'Gujrat',
    description:
        'Nageshwar Temple, located in Dwarka, Gujarat, India, is one of the twelve Jyotirlingas and a sacred Hindu shrine revered for its spiritual significance and historical importance as a revered abode of Lord Shiva, also known as Nageshwar Mahadev.',
    imageUrl:
        'https://upload.wikimedia.org/wikipedia/commons/thumb/2/22/Nageshwar.JPG/800px-Nageshwar.JPG',
    packagePrice: 22999,
  ),
  Temple(
    name: 'Trimbakeshwar',
    location: 'Maharashtra',
    description:
        'Trimbakeshwar Temple, located in Nashik, Maharashtra, India, is one of the twelve Jyotirlingas and a sacred Hindu shrine revered for its spiritual significance and historical importance as a revered abode of Lord Shiva, situated near the origin of the Godavari River.',
    imageUrl:
        'https://upload.wikimedia.org/wikipedia/commons/1/12/Trimbakeshwar_Temple-Nashik-Maharashtra-1.jpg',
    packagePrice: 2999,
  ),
  Temple(
    name: 'Bhimashankar',
    location: 'Maharashtra',
    description:
        'Bhimashankar Temple, located in Pune, Maharashtra, India, is one of the twelve Jyotirlingas and a sacred Hindu shrine revered for its spiritual significance and breathtaking natural surroundings, situated in the Sahyadri hills.',
    imageUrl:
        'https://upload.wikimedia.org/wikipedia/commons/d/d7/Bhimashankar.jpg',
    packagePrice: 999,
  ),
  Temple(
    name: 'Grishneshwar',
    location: 'Maharashtra',
    description:
        'Grishneshwar Temple, located in Aurangabad, Maharashtra, India, is one of the twelve Jyotirlingas and a sacred Hindu shrine revered for its spiritual significance and historical importance, situated near the famous Ellora Caves.',
    imageUrl:
        'https://upload.wikimedia.org/wikipedia/commons/a/ad/Grishneshwar_temple_in_Aurangabad_district.jpg',
    packagePrice: 3999,
  ),
  Temple(
    name: 'Omkareshwar',
    location: 'Madhya pradesh',
    description:
        'the Omkareshwar Temple, the jyortlinga is described a "roundish black stone" representing the form of Shiva and near it is a white stone representing Shivas consort, Parvati.',
    imageUrl:
        'https://upload.wikimedia.org/wikipedia/commons/0/01/Omkareswar_Jyotirlinga.jpg',
    packagePrice: 22999,
  ),
  // Add remaining temples similarly
];

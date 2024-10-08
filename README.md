import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: FoodCarousel(),
    );
  }
}

class FoodCarousel extends StatefulWidget {
  @override
  _FoodCarouselState createState() => _FoodCarouselState();
}

class _FoodCarouselState extends State<FoodCarousel> {
  final List<Map<String, String>> dishes = [
    {
      "name": "Шашлычный Фейерверк",
      "rating": "10",
      "description": "Погрузитесь в незабываемый вкус ...",
      "imageUrl": "https://static.tildacdn.com/stor3566-3630-4638-b839-376132343862/61296412.jpg",
    },
    {
      "name": "Стейк Погружение",
      "rating": "9",
      "description": "Нежно-мраморный кусок мяса, ...",
      "imageUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSI_12Yf_ELhUGjWXTZWiFWS8FnPYA5XWuijw&s",
    },
    {
      "name": "Шаурма Мастера Вкуса",
      "rating": "7",
      "description": "Лепешка, наполненная сочным мясом, ...",
      "imageUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSWpQiWpKybZyTMOJIl10Ojhp0_i9BWM7QJWA&s",
    },
    {
      "name": "Люля Кебаб Романтика Вкуса",
      "rating": "10",
      "description": "Нежные мясные котлеты, ...",
      "imageUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR46568Rs9eN2THtU8LO2qbimrwtjpIFHRerQ&s",
    },
  ];

  PageController _pageController = PageController();
  int _currentIndex = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: [
          Expanded(
            child: PageView.builder(
              controller: _pageController,
              itemCount: dishes.length,
              onPageChanged: (index) {
                setState(() {
                  _currentIndex = index;
                });
              },
              itemBuilder: (context, index) {
                final dish = dishes[index];
                return Stack(
                  alignment: Alignment.bottomCenter,
                  children: [
                    Image.network(
                      dish["imageUrl"]!,
                      fit: BoxFit.cover,
                      width: double.infinity,
                      height: double.infinity,
                    ),
                    Container(
                      height: 200,
                      color: Colors.black54, // Затемненный фон
                      child: Padding(
                        padding: const EdgeInsets.all(16.0),
                        child: Column(
                          mainAxisAlignment: MainAxisAlignment.end,
                          crossAxisAlignment: CrossAxisAlignment.start, // Выровненный по левой стороне
                          children: [
                            Text(
                              dish["name"]!,
                              style: TextStyle(
                                fontSize: 32,
                                color: Colors.white,
                                fontWeight: FontWeight.bold,
                              ),
                              textAlign: TextAlign.start, // Выровненный текст
                            ),
                            Text(
                              "Рейтинг: ${dish["rating"]}/10",
                              style: TextStyle(
                                fontSize: 18,
                                color: Colors.white,
                              ),
                              textAlign: TextAlign.start,
                            ),
                            ExpandableDescription(dish["description"]!),
                          ],
                        ),
                      ),
                    ),
                    Positioned(
                      right: 16,
                      top: 16,
                      child: Text(
                        "${index + 1}/${dishes.length}",
                        style: TextStyle(
                          fontSize: 16,
                          color: Colors.white,
                          fontWeight: FontWeight.w600,
                        ),
                      ),
                    ),
                  ],
                );
              },
            ),
          ),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              IconButton(
                icon: Icon(Icons.arrow_back),
                onPressed: _currentIndex > 0
                    ? () {
                        _pageController.previousPage(
                          duration: Duration(milliseconds: 300),
                          curve: Curves.easeIn,
                        );
                      }
                    : null,
              ),
              IconButton(
                icon: Icon(Icons.arrow_forward),
                onPressed: _currentIndex < dishes.length - 1
                    ? () {
                        _pageController.nextPage(
                          duration: Duration(milliseconds: 300),
                          curve: Curves.easeIn,
                        );
                      }
                    : null,
              ),
            ],
          ),
        ],
      ),
    );
  }
}

class ExpandableDescription extends StatefulWidget {
  final String description;

  ExpandableDescription(this.description);

  @override
  _ExpandableDescriptionState createState() => _ExpandableDescriptionState();
}

class _ExpandableDescriptionState extends State<ExpandableDescription> {
  bool _isExpanded = false;

  @override
  Widget build(BuildContext context) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start, // Выровненный по левой стороне
      children: [
        Text(
          _isExpanded ? widget.description : widget.description.split('.').first + '.',
          style: TextStyle(
            color: Colors.white,
            fontSize: 16,
          ),
          textAlign: TextAlign.start,
        ),
        GestureDetector(
          onTap: () {
            setState(() {
              _isExpanded = !_isExpanded;
            });
          },
          child: Text(
            _isExpanded ? 'Скрыть' : 'Подробнее',
            style: TextStyle(
              color: Colors.blue,
              fontSize: 16,
              fontWeight: FontWeight.bold,
            ),
          ),
        ),
      ],
    );
  }
}
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: FoodCarousel(),
    );
  }
}

class FoodCarousel extends StatefulWidget {
  @override
  _FoodCarouselState createState() => _FoodCarouselState();
}

class _FoodCarouselState extends State<FoodCarousel> {
  final List<Map<String, String>> dishes = [
    {
      "name": "Шашлычный Фейерверк",
      "rating": "10",
      "description": "Погрузитесь в незабываемый вкус ...",
      "imageUrl": "https://static.tildacdn.com/stor3566-3630-4638-b839-376132343862/61296412.jpg",
    },
    {
      "name": "Стейк Погружение",
      "rating": "9",
      "description": "Нежно-мраморный кусок мяса, ...",
      "imageUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSI_12Yf_ELhUGjWXTZWiFWS8FnPYA5XWuijw&s",
    },
    {
      "name": "Шаурма Мастера Вкуса",
      "rating": "7",
      "description": "Лепешка, наполненная сочным мясом, ...",
      "imageUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSWpQiWpKybZyTMOJIl10Ojhp0_i9BWM7QJWA&s",
    },
    {
      "name": "Люля Кебаб Романтика Вкуса",
      "rating": "10",
      "description": "Нежные мясные котлеты, ...",
      "imageUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR46568Rs9eN2THtU8LO2qbimrwtjpIFHRerQ&s",
    },
  ];

  PageController _pageController = PageController();
  int _currentIndex = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: [
          Expanded(
            child: PageView.builder(
              controller: _pageController,
              itemCount: dishes.length,
              onPageChanged: (index) {
                setState(() {
                  _currentIndex = index;
                });
              },
              itemBuilder: (context, index) {
                final dish = dishes[index];
                return Stack(
                  alignment: Alignment.bottomCenter,
                  children: [
                    Image.network(
                      dish["imageUrl"]!,
                      fit: BoxFit.cover,
                      width: double.infinity,
                      height: double.infinity,
                    ),
                    Container(
                      height: 200,
                      color: Colors.black54, // Затемненный фон
                      child: Padding(
                        padding: const EdgeInsets.all(16.0),
                        child: Column(
                          mainAxisAlignment: MainAxisAlignment.end,
                          crossAxisAlignment: CrossAxisAlignment.start, // Выровненный по левой стороне
                          children: [
                            Text(
                              dish["name"]!,
                              style: TextStyle(
                                fontSize: 32,
                                color: Colors.white,
                                fontWeight: FontWeight.bold,
                              ),
                              textAlign: TextAlign.start, // Выровненный текст
                            ),
                            Text(
                              "Рейтинг: ${dish["rating"]}/10",
                              style: TextStyle(
                                fontSize: 18,
                                color: Colors.white,
                              ),
                              textAlign: TextAlign.start,
                            ),
                            ExpandableDescription(dish["description"]!),
                          ],
                        ),
                      ),
                    ),
                    Positioned(
                      right: 16,
                      top: 16,
                      child: Text(
                        "${index + 1}/${dishes.length}",
                        style: TextStyle(
                          fontSize: 16,
                          color: Colors.white,
                          fontWeight: FontWeight.w600,
                        ),
                      ),
                    ),
                  ],
                );
              },
            ),
          ),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              IconButton(
                icon: Icon(Icons.arrow_back),
                onPressed: _currentIndex > 0
                    ? () {
                        _pageController.previousPage(
                          duration: Duration(milliseconds: 300),
                          curve: Curves.easeIn,
                        );
                      }
                    : null,
              ),
              IconButton(
                icon: Icon(Icons.arrow_forward),
                onPressed: _currentIndex < dishes.length - 1
                    ? () {
                        _pageController.nextPage(
                          duration: Duration(milliseconds: 300),
                          curve: Curves.easeIn,
                        );
                      }
                    : null,
              ),
            ],
          ),
        ],
      ),
    );
  }
}

class ExpandableDescription extends StatefulWidget {
  final String description;

  ExpandableDescription(this.description);

  @override
  _ExpandableDescriptionState createState() => _ExpandableDescriptionState();
}

class _ExpandableDescriptionState extends State<ExpandableDescription> {
  bool _isExpanded = false;

  @override
  Widget build(BuildContext context) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start, // Выровненный по левой стороне
      children: [
        Text(
          _isExpanded ? widget.description : widget.description.split('.').first + '.',
          style: TextStyle(
            color: Colors.white,
            fontSize: 16,
          ),
          textAlign: TextAlign.start,
        ),
        GestureDetector(
          onTap: () {
            setState(() {
              _isExpanded = !_isExpanded;
            });
          },
          child: Text(
            _isExpanded ? 'Скрыть' : 'Подробнее',
            style: TextStyle(
              color: Colors.blue,
              fontSize: 16,
              fontWeight: FontWeight.bold,
            ),
          ),
        ),
      ],
    );
  }
}
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: FoodCarousel(),
    );
  }
}

class FoodCarousel extends StatefulWidget {
  @override
  _FoodCarouselState createState() => _FoodCarouselState();
}

class _FoodCarouselState extends State<FoodCarousel> {
  final List<Map<String, String>> dishes = [
    {
      "name": "Шашлычный Фейерверк",
      "rating": "10",
      "description": "Погрузитесь в незабываемый вкус ...",
      "imageUrl": "https://static.tildacdn.com/stor3566-3630-4638-b839-376132343862/61296412.jpg",
    },
    {
      "name": "Стейк Погружение",
      "rating": "9",
      "description": "Нежно-мраморный кусок мяса, ...",
      "imageUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSI_12Yf_ELhUGjWXTZWiFWS8FnPYA5XWuijw&s",
    },
    {
      "name": "Шаурма Мастера Вкуса",
      "rating": "7",
      "description": "Лепешка, наполненная сочным мясом, ...",
      "imageUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSWpQiWpKybZyTMOJIl10Ojhp0_i9BWM7QJWA&s",
    },
    {
      "name": "Люля Кебаб Романтика Вкуса",
      "rating": "10",
      "description": "Нежные мясные котлеты, ...",
      "imageUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR46568Rs9eN2THtU8LO2qbimrwtjpIFHRerQ&s",
    },
  ];

  PageController _pageController = PageController();
  int _currentIndex = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: [
          Expanded(
            child: PageView.builder(
              controller: _pageController,
              itemCount: dishes.length,
              onPageChanged: (index) {
                setState(() {
                  _currentIndex = index;
                });
              },
              itemBuilder: (context, index) {
                final dish = dishes[index];
                return Stack(
                  alignment: Alignment.bottomCenter,
                  children: [
                    Image.network(
                      dish["imageUrl"]!,
                      fit: BoxFit.cover,
                      width: double.infinity,
                      height: double.infinity,
                    ),
                    Container(
                      height: 200,
                      color: Colors.black54, // Затемненный фон
                      child: Padding(
                        padding: const EdgeInsets.all(16.0),
                        child: Column(
                          mainAxisAlignment: MainAxisAlignment.end,
                          crossAxisAlignment: CrossAxisAlignment.start, // Выровненный по левой стороне
                          children: [
                            Text(
                              dish["name"]!,
                              style: TextStyle(
                                fontSize: 32,
                                color: Colors.white,
                                fontWeight: FontWeight.bold,
                              ),
                              textAlign: TextAlign.start, // Выровненный текст
                            ),
                            Text(
                              "Рейтинг: ${dish["rating"]}/10",
                              style: TextStyle(
                                fontSize: 18,
                                color: Colors.white,
                              ),
                              textAlign: TextAlign.start,
                            ),
                            ExpandableDescription(dish["description"]!),
                          ],
                        ),
                      ),
                    ),
                    Positioned(
                      right: 16,
                      top: 16,
                      child: Text(
                        "${index + 1}/${dishes.length}",
                        style: TextStyle(
                          fontSize: 16,
                          color: Colors.white,
                          fontWeight: FontWeight.w600,
                        ),
                      ),
                    ),
                  ],
                );
              },
            ),
          ),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              IconButton(
                icon: Icon(Icons.arrow_back),
                onPressed: _currentIndex > 0
                    ? () {
                        _pageController.previousPage(
                          duration: Duration(milliseconds: 300),
                          curve: Curves.easeIn,
                        );
                      }
                    : null,
              ),
              IconButton(
                icon: Icon(Icons.arrow_forward),
                onPressed: _currentIndex < dishes.length - 1
                    ? () {
                        _pageController.nextPage(
                          duration: Duration(milliseconds: 300),
                          curve: Curves.easeIn,
                        );
                      }
                    : null,
              ),
            ],
          ),
        ],
      ),
    );
  }
}

class ExpandableDescription extends StatefulWidget {
  final String description;

  ExpandableDescription(this.description);

  @override
  _ExpandableDescriptionState createState() => _ExpandableDescriptionState();
}

class _ExpandableDescriptionState extends State<ExpandableDescription> {
  bool _isExpanded = false;

  @override
  Widget build(BuildContext context) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start, // Выровненный по левой стороне
      children: [
        Text(
          _isExpanded ? widget.description : widget.description.split('.').first + '.',
          style: TextStyle(
            color: Colors.white,
            fontSize: 16,
          ),
          textAlign: TextAlign.start,
        ),
        GestureDetector(
          onTap: () {
            setState(() {
              _isExpanded = !_isExpanded;
            });
          },
          child: Text(
            _isExpanded ? 'Скрыть' : 'Подробнее',
            style: TextStyle(
              color: Colors.blue,
              fontSize: 16,
              fontWeight: FontWeight.bold,
            ),
          ),
        ),
      ],
    );
  }
}

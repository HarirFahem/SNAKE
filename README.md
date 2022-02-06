# Final Project
## Snake Game
create a MainWindow based application using the designer
- [Credit](#credit)
- [Introduction](#INTRO)
- [OverView](#overview)
- [Steps](#Steps)
- [Conclusion](#conclusion)

<div id = "back"></div>


### **Credit**

<a name="credit"></a>

We cannot deny that we have made a huge effort to realize this project. However, this would not have been possible without your support and help, we would like to express our sincere thanks to you.

By way of recognition, we would like to thank, very sincerely, Mr **BELCAID Anass**, for his quality supervision, his professional motivation, his advice and constructive criticism, his corrections, his kindness, and his patience as well as for the time he has dedicated to carrying out this work.

We would like to thank you again for your careful reading of this report, as well as for the comments you will make us during the defense to improve our work. 

Finally, we would like to warmly thank our training director as well as the entire teaching team of EIDIA Euromed who gave us an incredible opportunity to be able to work on this type of project, to prepare us for the professional world in general.


### **Introduction** 

<a name="INTRO"></a>

"" **You might not think that programmers are artists, but programming is an extremely creative profession. It's logic-based creativity.** ""

The **QGraphicsView class** provides a widget for displaying the contents of a QGraphicsScene. QGraphicsView visualizes the contents of a QGraphicsScene in a scrollable viewport. To create a scene with geometrical items, see QGraphicsScene's documentation. QGraphicsView is part of the Graphics View Framework.

![Image](/Qgraphicview.png)

The **QGraphicsScene class** provides a surface for managing a large number of 2D graphical items. The class serves as a container for QGraphicsItems. It is used together with QGraphicsView for visualizing graphical items, such as lines, rectangles, text, or even custom items, on a 2D surface. QGraphicsScene is part of the Graphics View Framework. It also provides functionality that lets you efficiently determine both the location of items, and for determining what items are visible within an arbitrary area on the scene. With the QGraphicsView widget, you can either visualize the whole scene, or zoom in and view only parts of the scene. 

The **QGraphicsItem class** is the base class for all graphical items in a QGraphicsScene. It provides a light-weight foundation for writing your own custom items. This includes defining the item's geometry, collision detection, its painting implementation and item interaction through its event handlers. QGraphicsItem is part of the Graphics View Framework.

![Image](/Qgraphicsitem.png)

The **QMediaPlayer class** allows the playing of a media source. It is a high level media playback class. It can be used to playback such content as songs, movies and internet radio. The content to playback is specified as a QMediaContent object, which can be thought of as a main or canonical URL with additional information attached. When provided with a QMediaContent playback may be able to commence.

![Image](/Qmediaplayer.png)

The **QMediaPlaylist class** provides a list of media content to play. It is intended to be used with other media objects, like QMediaPlayer. It allows to access the service intrinsic playlist functionality if available, otherwise it provides the local memory playlist implementation.

![Image](/Qmediaplaylist.png)


 >**In This Zip we have the SnakeGameProject** [FinalProject.zip](https://github.com/HarirFahem/Final-Project/blob/main/FinalProject.zip) 
 
### **OverView**

[(**Back to top**)](#back)

<a name="overview"></a>
This project is a very important experience for us EIDIA students to become familiar with these new materials that we can consider very important.

During this period, the project that we are going to carry out is an game named **Snake Game**. To clarify things for you, and to bring you closer to the options offered by our project, we have written this report which contains all the details and explanations associated with our project.

  To achieve Snake Game, we used Qt-Creator which is a cross-platform integrated development environment (IDE) built for the maximum developer experience. Qt Creator runs on Windows, Linux, and macOS desktop operating systems, and allows developers to create applications across desktop, mobile, and embedded platforms.
  
  **Snake Game** is a video game that originated during the late 1970s in arcades becoming something of a classic. It became the standard pre-loaded game on Nokia phones in 1998.The player controls a long, thin creature, resembling a snake, which roams around on a bordered plane, picking up food (or some other item), trying to avoid hitting its own tail or the edges of the playing area. Each time the snake eats a piece of food, its tail grows longer, making the game increasingly difficult. The user controls the direction of the snake's head (**up, down, left, or right**), and the snake's body follows.
  
  Here is a overview of how it is designed:

  
  When we click on play , this interface is shown: 
  
  ![Image](/backgroundsnake.png)
 
  
   ### **Steps** 
  
 <a name="Steps"></a> 
  In carrying out this project, we had several Steps, thanks to which we were able to frame our work, and do our research in a well-organized way.
  
The steps that have been set to carry out this work are the following:

First We create our window , it will be a GraphicsScene with its own properties , and we generate the first class which we called MainWindow:
Firstly ,We create our first window (game.h) :
```javascript
class Game:public QGraphicsView
{
public:
    Game(QWidget * parent =0);
    void keyPressEvent(QKeyEvent *event);
    void Menu(QString title, QString Play);
    void gameOver();

    QGraphicsScene *gameScene;
    QGraphicsTextItem *titleText;

public slots:
    void start();
     void AboutSlot();
private:
    QPushButton * newgame;
    QPushButton * About;
    QPushButton * Quit ;

};

```
we implement this methods in the game.cpp:
We add a image for our background:
```javascript
Game::Game(QWidget *parent):QGraphicsView(parent)
{
 
   setFixedSize(1400,850);
    gameScene = new QGraphicsScene(this);
    gameScene->setSceneRect(0,0,1400,850);
    QGraphicsPixmapItem *bg = new QGraphicsPixmapItem();
    bg->setPixmap(QPixmap(":/aSnake.png").scaled(1400,880));
      gameScene->addItem(bg);
      setScene(gameScene);
 }
 ```
 Then we display our Menu which contains three Push Button , each one have its connections:
 ```javascript
void Game::Menu(QString title,QString play)
{
  //Create the title
    titleText = new QGraphicsTextItem(title);
    QFont titleFont("arial" , 50);
    titleText->setFont( titleFont);
    titleText->setPos(width()/2 - titleText->boundingRect().width()/2,200);
    gameScene->addItem(titleText);
    newgame = new QPushButton(play);
    newgame->setGeometry(QRect(QPoint(width()/2- titleText->boundingRect().width()/4, 400), QSize(250, 70)));
      gameScene->addWidget(newgame);

    About = new QPushButton("About");
     About->setGeometry(QRect(QPoint(width()/2- titleText->boundingRect().width()/4, 500), QSize(250, 70)));
   gameScene->addWidget(About);
   Quit = new QPushButton("Quit");
     Quit->setGeometry(QRect(QPoint(width()/2- titleText->boundingRect().width()/4, 600), QSize(250, 70)));
     gameScene->addWidget(Quit);
// connections
connect(newgame,SIGNAL(clicked()) , this , SLOT(start()));
connect(Quit,SIGNAL(clicked()) , this , SLOT(close()));
connect(About,SIGNAL(clicked()) , this , SLOT(AboutSlot()));

}
```

  Here is the first interface shown is:
  
  ![Image](/frontend.png)
  
  
[(**Back to top**)](#back)

- The first button *Start* move us to the game.

  ![Image](/backgroundsnake.png)

  We created two classes called MoveSnake and SnakePart which are responsible for the Snake and its funcionality. 
  
As we mentioned in the Overview, the Snake move in the four directions and we control them from the keyPress Event:
* Down or X
* Up or Z
* Right or D
* Left or Q
  
```javascript
void SnakeMove::keyPressEvent(QKeyEvent *event)
{

    if(( event->key() == Qt::Key_Down || event->key()== Qt::Key_X) && sHead->getDirection() != "UP") {
        direction = "DOWN";
    }
    else if(( event->key() == Qt::Key_Up || event->key()== Qt::Key_Z) &&sHead->getDirection() != "DOWN") {
        direction = "UP";
    }
    else if((event->key() == Qt::Key_Right || event->key()== Qt::Key_D) && sHead->getDirection() != "LEFT") {
        direction = "RIGHT";
    }
    else if((event->key() == Qt::Key_Left || event->key()== Qt::Key_Q) && sHead->getDirection() != "RIGHT") {

        direction = "LEFT";
    }
```

Then we connect these directions with the movement of the Snake , also we let our snake cross the edge of the board :

```javascript
void SnakePart::move() {
    static int first;

    if (direction == "DOWN"  )
        this->setY(this->y()+40);
    else if(direction == "UP")
        this->setY(this->y()-40);
    else if(direction == "LEFT")
        this->setX(this->x()-40);
    else if(direction == "RIGHT")
        this->setX(this->x()+40);
    if(this->getForward()!= NULL)
        direction = this->getForward()->direction;
    if(first){
    if(this->y() >= 880 ){
        this->setY(0);
    }
    else if(this->y()<0){
        this->setY(880);
    }
    else if(this->x() < 0){
        this->setX(1400);
    }
    else if(this->x() >= 1400){
        this->setX(0);
    }

    }
    first++;
}
void SnakePart::addBehind() {
    int x;
    int y;

    if(this->getForward()->getDirection() == "UP"){
        x = this->getForward()->x();
        y = this->getForward()->y() + 40;
    }
    else if(this->getForward()->getDirection() == "DOWN"){
        x = this->getForward()->x();
        y = this->getForward()->y() - 40;
    }
    else if(this->getForward()->getDirection() == "RIGHT"){
        y = this->getForward()->y();
        x = this->getForward()->x() - 40;
    }
    else if(this->getForward()->getDirection() == "LEFT"){
        y = this->getForward()->y();
        x = this->getForward()->x() + 40;
    }
    setPos(x,y);
}

```
![Image](/Edges.png)

Snake cross the edge of the board

When we clicked *Start* First, a snake starts at the (200,200) of the Window moving Right, we press space if we want to play 

```javascript

    snakeHead = new SnakePart(this);
    snakeHead->setForward(NULL);
    snakeHead->setBackward(NULL);
    snakeHead->setPos(200,200);
    snakeHead->setDirection("RIGHT");
    snakeHead->part = "HEAD";
    snakeHead->setImage();
    snakeTail = snakeHead;

    direction = "RIGHT";

    addPart();
    addPart();
    addPart();

    text = new QGraphicsTextItem(this);
    text->setVisible(true);
    text->setPlainText("Press Space to continue");
    text->setDefaultTextColor(Qt::lightGray);
    text->setPos(650,250);
    text->setFont(QFont("",14));
```

[(**Back to top**)](#back)

 We used a function called *setImage* to draw our snake by parts
  
  ```javascript
  
  void SnakePart::setImage() {
    if(part == "HEAD"){

        if(direction == "UP"){
     setPixmap(QPixmap(":/headup.png").scaled(40,40));
        }else if(direction == "DOWN"){
           setPixmap(QPixmap(":/headDown.png").scaled(40,40));
        }else if(direction == "LEFT"){
            setPixmap(QPixmap(":/headLeft.png").scaled(40,40));
        }else if(direction == "RIGHT"){
            setPixmap(QPixmap(":/head.png").scaled(40,40,Qt::KeepAspectRatio));
        }

}
    else if(part == "TAIL") {
        if(direction == "UP"){
          setPixmap(QPixmap(":/atailUp.png").scaled(40,40));
        }else if(direction == "DOWN"){
           setPixmap(QPixmap(":/atailDown.png").scaled(40,40));
        }else if(direction == "LEFT"){
            setPixmap(QPixmap(":atail.png").scaled(40,40));
        }else if(direction == "RIGHT"){

            setPixmap(QPixmap(":/atailLeft.png").scaled(40,40));
        }
    }
    else if (part == "PART"){
        if(direction == this->backward->getDirection()){
        if(direction == "LEFT" ||direction ==  "RIGHT")
            setPixmap(QPixmap(":/left-right.png").scaled(40,40));
        else if (direction == "UP" || direction == "DOWN")
            setPixmap(QPixmap(":/aup-down.png").scaled(40,40));
}
        else{
            if((direction == "UP" && this->backward->getDirection() == "LEFT")
                    || (direction == "RIGHT" && this->backward->getDirection() == "DOWN"))
                setPixmap(QPixmap(":/leftUp-downRight.png").scaled(40,40));
            else if((direction == "UP" && this->backward->getDirection() == "RIGHT")
                    || (direction == "LEFT" && this->backward->getDirection() == "DOWN"))
                setPixmap(QPixmap(":/rightUp-downLeft.png").scaled(40,40));
            else if((direction == "LEFT" && this->backward->getDirection() == "UP")
                    || (direction == "DOWN" && this->backward->getDirection() == "RIGHT"))
                setPixmap(QPixmap(":/aupLeft-rightDown.png").scaled(40,40));
            else
                setPixmap(QPixmap(":/aupRight-leftDown.png").scaled(40,40));
 }  }
}

  ```
When we press on the keyboard, the movement of the snake is in relation with the key clicked:
here is the function that we used: 

```javascript

void MoveSnake::move() {
    snakeHead->setDirection(direction);
    moveSnake();

}
void MoveSnake::addPart(){
    SnakePart *part = new SnakePart(this);
    SnakePart *temp = snakeHead;
    while(temp->getBackward() != NULL) {
        temp = temp->getBackward();
    }
    temp->setBackward( part);
    part->setForward( temp);
    part->setBackward(NULL);
    part->addBehind();
    part->setDirection(temp->getDirection());
    snakeTail = part;
    part->part = "TAIL";
    if(temp != snakeHead)
    temp->part = "PART";
    part->setImage();
    temp->setImage();
}

void MoveSnake::moveSnake()
{

   SnakePart *temp = snakeTail;

   while(temp!=NULL) {

       temp->move();
       temp = temp->getForward();
   }
}

```

We move to the food, We create a class called Food for generate our food and also the Bombs

The header part of the food class called food.h , here is the code that we generate:

*food.h*

```javascript
class food:public QGraphicsPixmapItem
{
public:
    food(QGraphicsItem *parent = 0,QString name = "");
    int score;
};
class Bomb:public QGraphicsPixmapItem
{
public:
    Bomb(QGraphicsItem *parent = 0);
    int score;
};


```

When the snake "eats" a strawberry or kiwi, it score increase, But if it's an egg it decrease by 5.

Here is the implementation of the food class:

*(Food.cpp)*

```javascript

food::food(QGraphicsItem *parent,QString name):QGraphicsPixmapItem(parent)
{
    if(name == "strawberry"){
        setPixmap(QPixmap(":/Fruit.png").scaled(60,60));
        score = 2;
    }else if(name == "Egg"){
        setPixmap(QPixmap(":/egg.png").scaled(60,60));
        score = -5;
    }
    else{
        setPixmap(QPixmap(":/Fruit1.png").scaled(60,60,Qt::KeepAspectRatio));
        score = 5;
    }
}
Bomb::Bomb(QGraphicsItem *parent):QGraphicsPixmapItem(parent){


        setPixmap(QPixmap(":/Bomb.png").scaled(60,60));

}
```
![Image](/Fruits.png)

Fruits illustration

[(**Back to top**)](#back)

Our food: "Strawberry , Kiwi, and Egg" appears at random locations, also our Bombs
Here is the function that is responsible for the random locations of the meal:

```javascript
MoveSnake::MoveSnake(QGraphicsItem *parent):QGraphicsRectItem(parent)
{
t = new QTimer();
   connect(t,SIGNAL(timeout()),this,SLOT(move()));

    foodTimer = new QTimer();
    connect(foodTimer,SIGNAL(timeout()),this,SLOT(makeFood()));

    food1Timer = new QTimer();
    connect(food1Timer,SIGNAL(timeout()),this,SLOT(makeFood1()));


    food2Timer = new QTimer();
    connect(food2Timer,SIGNAL(timeout()),this,SLOT(makeFood2()));
    
    BombTimer = new QTimer();
     connect(BombTimer,SIGNAL(timeout()),this,SLOT(makeBomb()));
    }
void MoveSnake::makeFood()
{
    food * f1 = new food(this,"strawberry");
    f1->setX(qrand() % (1400/40)* 40);
    f1->setY(qrand() % (880/40) * 40) ;

}
void MoveSnake::makeFood1()
{
    food * f1 = new food(this);
    f1->setX(qrand() % (1400/40)* 40);
    f1->setY(qrand() % (880/40) * 40) ;

}
void MoveSnake::makeFood2()
{
    food * f1 = new food(this,"Egg");
    f1->setX(qrand() % (1400/40)* 40);
    f1->setY(qrand() % (880/40) * 40) ;
}
void MoveSnake::makeBomb(){
    Bomb * f1 = new Bomb(this);
    f1->setX(qrand() % (1400/40)* 40);
    f1->setY(qrand() % (880/40) * 40) ;
}
```
After clicking on the button play, we should press on space to start playing.
When we press Space, the snake move and the food appear with a certain timing, but when we press space the game stop.

Here is the class that is generated for appearing the fruits :

```javascript
void MoveSnake::keyPressEvent(QKeyEvent *event)
{
if(event->key() == Qt::Key_Space){
        if(t->isActive()){
            foodTimer->stop();
            food1Timer->stop();
            food2Timer->stop();
            BombTimer->stop();

        t->stop();
        text->setVisible(true);

        }
        else{

            foodTimer->start(2000);
            food1Timer->start(6000);
            food2Timer->start(10000);
            BombTimer->start(80000);
            t->start(60);

            text->setVisible(false);
        }

    }
}

```

When the snake "eats" a Food, it gets longer, we check the collidingItems in our class SnakePart, the game continues until the snake "dies".A snake dies by either eating a bomb, or by running into its own tail.

Here is the function of checkcolliding: 

```javascript
void SnakePart::checkColliding() {
    QList <QGraphicsItem *> coll = this->collidingItems();

   for(int i = 0,n = coll.length(); i < n; i++) {
        food *f = dynamic_cast<food *>(coll[i]);
         Bomb *b = dynamic_cast<Bomb *>(coll[i]);
        if(f) {
            QPointF thisCenter(x()+10,y()+10);
            QPointF foodCenter(f->x()+10,f->y()+10);
            QLineF ln(thisCenter,foodCenter);
            if(ln.length() == 0){
           
                game->snake->addPart();
                game->snake->addPart();
           game->gameScene->removeItem(f);
           game->score->setScore(game->score->getScore()+f->score);
           delete f;
	   }
	   }else if(b) {
            QPointF thisCenter(x()+10,y()+10);
            QPointF BombCenter(b->x()+10,b->y()+10);
            QLineF ln(thisCenter,BombCenter);
            if(ln.length() == 0){
                   game->gameOver();
        }}
        else if(coll[i]) {
            if(typeid(*coll[i])== typeid(SnakePart))
            game->gameOver();
            return;
        }
}
```

![Image](/eatbomb.png)

Eating a Bomb

![Image](/eatSelf.png)

Pass Away by Eating its Self 

[(**Back to top**)](#back)

The final score is based on the number of Food eaten by the snake,and we save the high Score for giving the challenge:
Here is th header file:

*(Score.h)*

```javascript

class Score:public QGraphicsTextItem
{
public:
    Score(QGraphicsItem *parent = 0);
    int getScore() ;
    void setScore(int value);

private:
    int score;

};

class HighScore:public QGraphicsTextItem
{
public:
    HighScore(QGraphicsItem *parent = 0);
    int getScore();
    void setScore(int value);

private:
    int highscore;
};
```

And in the cpp file we implement our methods:

*(Score.cpp)

```javascript
Score::Score(QGraphicsItem *parent):QGraphicsTextItem(parent)
{
    score = 0;

    setPos(5,10);
    setFont( QFont("",30));
    setDefaultTextColor(Qt::lightGray);
}

int Score::getScore()
{
    return score;
}

void Score::setScore(int value)
{
    score = value;
    setPlainText("Score: " + QString::number(score));

}

HighScore::HighScore(QGraphicsItem *parent):QGraphicsTextItem(parent)
{
    highscore = 0;
    setPos(5,50);
    setFont( QFont("",30));
    setDefaultTextColor(Qt::lightGray);
}
int HighScore::getScore()
{
    return highscore;
}

void HighScore::setScore(int value)
{
    highscore = value;
    setPlainText("High Score: " + QString::number(highscore));
}
```

![Image](/HighScore.png)

HighScore acheived 

We add finally the music to our game by the QMediaPlaylist, we have 3 sounds: one for playing,second for eating and the third and the last one for losing :

```javascript

m_player = new QMediaPlayer();
    m_playlist = new QMediaPlaylist(m_player);

   m_player->setPlaylist(m_playlist);
   m_playlist->addMedia(QUrl("qrc:/eat.wav"));
   m_playlist->setPlaybackMode(QMediaPlaylist::CurrentItemOnce);
```

We play or stop our sound compared to the situation:

```javascript
     m_player->stop();
Or
    m_player->play();
```

-  The second is for more informations about our game.
  
  If we pressed this button, they will show the window bellow:
  
  ![Image](/about.png)
  
  If We choose to know info about the game , we will see thiw window:
  
 ![Image](/Aboutsnake.png)
  
-  The last one is to close the Game.
 
 we add the closeEvent for saving highScores in a txt file:
 
```javascript
void Game::closeEvent(QCloseEvent *e){
    QFile file("/Users/hp/Desktop/sav.txt");
    if (file.open(QIODevice::ReadWrite| QIODevice::Text)){

        QTextStream out(&file);
        if(score->getScore() > highscore->getScore()) {
            out<<score->getScore()<<Qt::endl;
            file.close();
        }
    }
}
```

[(**Back to top**)](#back)

### **Conclusion**

<a name="conclusion"></a>


This project turned out to be very rewarding insofar as it consisted of a concrete approach to the engineering profession. Indeed, taking the initiative and respecting deadlines will be essential aspects of our future profession.
In addition, it allowed us to apply our knowledge to a practical area.

As well as during our work, we had a problem with our computer, it hangs completely and if we don't restart it by pushing the power button, it won't work. Despite all its difficulties, it helps us to know consistent values across the entire field studied, which we will probably be led to do in our future profession.

•	To summarize, this project is a very important experience for us to be familiar with this material and to develop our skills
Thank you Sir

 [(**Back to top**)](#back)
    
Made By:
* Khadija Fahem
* Wafa Harir

 


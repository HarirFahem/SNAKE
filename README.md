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


 >**In This Zip we have the SnakeGameProject** [FinalProject.zip]() 
 
### **OverView**

[(**Back to top**)](#back)

<a name="overview"></a>
This project is a very important experience for us EIDIA students to become familiar with these new materials that we can consider very important.
 	During this period, the project that we are going to carry out is an game named **Snake Game**
	To clarify things for you, and to bring you closer to the options offered by our project, we have written this report which contains all the details and explanations associated with our project.
  To achieve Snake Game, we used Qt-Creator which is a cross-platform integrated development environment (IDE) built for the maximum developer experience. Qt Creator runs on Windows, Linux, and macOS desktop operating systems, and allows developers to create applications across desktop, mobile, and embedded platforms.
  **Snake Game** is a video game that originated during the late 1970s in arcades becoming something of a classic. It became the standard pre-loaded game on Nokia phones in 1998.The player controls a long, thin creature, resembling a snake, which roams around on a bordered plane, picking up food (or some other item), trying to avoid hitting its own tail or the edges of the playing area. Each time the snake eats a piece of food, its tail grows longer, making the game increasingly difficult. The user controls the direction of the snake's head (**up, down, left, or right**), and the snake's body follows.
  Here is a overview of how it is designed:
  
  ![Image](/backgroundsnake.png)
  
 <a name="Steps"></a> 
  In carrying out this project, we had several Steps, thanks to which we were able to frame our work, and do our research in a well-organized way.
  
 ### **OverView** 
The steps that have been set to carry out this work are the following:
We create our window , it will be a GraphicsScene with its own properties , and we generate the first class which we called MainWindow:
Firstly ,We create our first window (MainWindow.h) :
```Cpp
class Mainwindow:public QGraphicsView
{
public:
    Mainwindow(QWidget * parent =0);
    void keyPressEvent(QKeyEvent *event);
    void Menu(QString title, QString Play);
    void gameOver();

    QGraphicsScene *Window;
    QGraphicsTextItem *Titre;

public slots:
    void start();
     void AboutSlot();
private:
    QPushButton * newgame;
    QPushButton * About;
    QPushButton * Quit ;

};

```
we implement this methods in the MainWindow.cpp:
We add a image for our background:
```Cpp
Mainwindow::Mainwindow(QWidget *parent):QGraphicsView(parent)
{
 
   setFixedSize(1400,850);
    Window = new QGraphicsScene(this);
    Window->setSceneRect(0,0,1400,850);
    QGraphicsPixmapItem *bg = new QGraphicsPixmapItem();
    bg->setPixmap(QPixmap(":/aSnake.png").scaled(1400,880));
      Window->addItem(bg);
      setScene(Window);
 }
 ```
 Then we display our Menu which contains three Push Button , each one have its connections:
 ```Cpp
void Game::displayMainMenu(QString title,QString play)
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
connect(About,SIGNAL(clicked()) , this , SLOT(Aboutslot()));

}
```
The first button Start move us to the game, the second is for more informations about our game, and the last one is to close the Game.
Secondly, we created two classes called SnakeMove and SnakePart which are responsible for the Snake and its funcionality. 
As we mentioned in the Overview, the Snake move in the four directions and we control them from the keyPress Event 
```Cpp
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

Then we connect these directions with the mouvement of the Snake in the class PartSnake :
```Cpp
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
>



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

 


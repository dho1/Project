#include <cstdio> // std
#include <cstring>
#include <iostream>
#include <sys/socket.h>
#include <netinet/in.h>
#include <fontconfig/fontconfig.h>
#include <SFML/Graphics.hpp>
#include "types.h"

using namespace std;

// Later iterations should pass this via struct pointer to init()
// Client networking will fill these values.

sf::Font MyFont;
vector<sf::RectangleShape> shapes;
vector<sf::Text>  lables;

sf::FloatRect towerButton;
sf::FloatRect creepButton;
sf::FloatRect topButton;
sf::FloatRect midButton;
sf::FloatRect botButton;

sf::FloatRect buttons[] = {towerButton, creepButton, topButton, midButton, botButton};

void update (sf::RenderWindow& window, sf::Clock& sclock);

void draw_hud()
{
    sf::RectangleShape shape(sf::Vector2f(800, 40));
    shape.setOutlineColor(sf::Color::White);
    shape.setOutlineThickness(2.0f);
    shape.setPosition(1, 559);
    shapes.push_back(shape);
}

void setup()
{
    sf::Text temp("Tower", MyFont, 20);
    lables.push_back(temp);
    
    temp.setString("Creep");
    lables.push_back(temp);
    
    temp.setString("Top Path");
    lables.push_back(temp);
    
    temp.setString("Mid Path");
    lables.push_back(temp);
    
    temp.setString("Bot Path");
    lables.push_back(temp);
}

void add_slot(int button) 
{
    sf::Text readytext(lables[button - 1].getString(), MyFont, 20);
    sf::RectangleShape shape(sf::Vector2f(100, 39));
   
    shape.setFillColor(sf::Color(140, 140, 140));
    shape.setOutlineColor(sf::Color::White);
    shape.setOutlineThickness(2.0f);
    
    lables[button - 1].setPosition(115 * button, 600 - 40);
    
    shape.setPosition(115 * button, 600 - 40);
    shapes.push_back(shape);
    buttons[button - 1] = shape.getGlobalBounds();
}

bool find_font (char ** path) 
{
    FcResult result;
    FcPattern* pat = FcPatternCreate();

    FcConfigSubstitute (0, pat, FcMatchPattern);
    FcDefaultSubstitute (pat);
    FcPattern * match =  FcFontMatch(NULL, pat, &result);
    match = FcFontMatch (0, pat, &result);
    return (FcPatternGetString(match, FC_FILE, 0, (FcChar8**)path) == FcResultMatch);
}

void * init () 
{
    sf::Clock sclock;
    sf::RenderWindow window(sf::VideoMode(800, 600), "SFML window");

    char * font_path;
    find_font( &font_path );

    if (!MyFont.loadFromFile(font_path)) 
    {
        printf("error loading font\n");
    }

    setup();
    draw_hud();

    for (int i = 1; i < 6; i++)
        add_slot(i);

    while (window.isOpen()) 
    {
        update(window, sclock);
    }
    return NULL;
}

void update (sf::RenderWindow& window, sf::Clock& sclock) 
{
    sf::Time elapsed = sclock.restart();
    ((void) elapsed); // silence warning for now.
    
    sf::Event event;
    while (window.pollEvent(event)) 
    {
        if (event.type == sf::Event::Closed)
            window.close();
        else if (event.type == sf::Event::MouseButtonPressed)
        {
            sf::Vector2f mouse = sf::Vector2f(sf::Mouse::getPosition(window));
        }
    }

    sf::Vector2f mouse = sf::Vector2f(sf::Mouse::getPosition(window));
    for (size_t i = 0; i < shapes.size(); ++i) 
    {
        if (shapes[i].getGlobalBounds().contains(mouse)) 
        {
            if (i != 0)
                shapes[i].setOutlineColor(sf::Color(255, 0,0));
        } else {
            shapes[i].setOutlineColor(sf::Color::White);
        }
    }

    window.clear();

    size_t i;
 
    for (i = 0; i < shapes.size(); ++i) 
    {
        window.draw(shapes[i]);
    }

    for (i = 0; i < lables.size(); ++i) 
    {
        window.draw(lables[i]);
    }

    window.display();
}

int main(int argc, char *argv[])
{
    init();
    return 0;
}

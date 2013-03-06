CFLAGS = -Wall -W -ansi -pedantic -g

all : hud

hud : hud.cpp
	g++ $(CFLAGS) hud.cpp -o hud -lfontconfig -lsfml-graphics -lsfml-window -lsfml-system

clean :
	rm -f hud *.o

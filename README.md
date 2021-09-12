# Cau_assignment
#include <bangtal>
using namespace bangtal;

int main()
{
	auto room1 = Scene::create("룸1", "Images/배경-1.png");
	auto room2 = Scene::create("룸2", "Images/배경-2.png");

	auto door1 = Object::create("Images/문-오른쪽-닫힘.png", room1, 800, 270);
	auto closed1 = true;


	auto key = Object::create("Images/열쇠.png", room1, 600, 150);
	key->setScale(0.2f);
	key->setOnMouseCallback([&](auto object, auto x, auto y, auto action) -> bool {
		object->pick();
		return true;
		});

	door1->setOnMouseCallback([&](auto object, auto x, auto y, auto action) -> bool {
		if (closed1) {
			if (key->isHanded()) {
				object->setImage("Images/문-오른쪽-열림.png");
				room2->enter();
				closed1 = false;
			}
			else {
				showMessage("열쇠를 가져와!");
			}
		}

		else {
			endGame();
		}

		return true;
		});

	startGame(room1);
}

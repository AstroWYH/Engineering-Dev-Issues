```c++
#include <deque>
#include <iostream>

void print_container(const std::deque<int>& c)
{
	for (int i : c)
		std::cout << i << " ";
	std::cout << '\n';
}

int main()
{
	deque<int> c;
	c.push_back(4);
	c.push_back(3);
	c.push_back(4);
	c.push_back(2);
	c.push_back(1);
	c.push_back(4);

	//print_container(c);
	for (int& i : c) {
		std::cout << "Start num:" << i << endl;
	}

	//c.erase(c.begin());
	//print_container(c);

	//c.erase(c.begin() + 2, c.begin() + 5);
	//print_container(c);

	for (std::deque<int>::iterator it = c.begin(); it != c.end();)
	{
		//print_container(c);
		if (*it == 4)
			it = c.erase(it); // 删除后会指向下一个元素，it不能放在for里，需要在这里赋值。
		else
			++it;
	}
	//std::remove_if(c.begin(), c.end(), [](int x)->bool { return x == 4; }); // 无法正常使用

	//print_container(c);
	for (int& i : c) {
		std::cout << "End num:" << i << endl;
	}
}
```


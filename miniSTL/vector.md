##vector

```c++
#include <iostream>
#include <algorithm>
#include <numeric>
#include <ostream>
#include <sys/types.h>

using namespace std;
namespace miniSTL
{
    template <typename T>
    class Vector
    {
        public:
            typedef T value_type;
            typedef T* iterator;

        private:
            value_type* _data;
            size_t _size;
            size_t _capacity;

        public:
            Vector():_data(nullptr), _size(0), _capacity(0){}
            ~Vector()
            {
                delete [] _data;
                _data = nullptr;
                _size = 0; 
                _capacity = 0;
            }

            Vector(const Vector& vec)
            {
                _size = vec._size;
                _capacity = vec._capacity;
                _data = new value_type[_capacity];
                for(int i = 0; i < _size; ++i)
                {
                    _data[i] = vec._data[i];
                }
            }

            Vector& operator=(const Vector& vec)
            {
                if(this == &vec)
                {
                    return *this;
                }
                value_type* temp = new value_type[vec._capacity];
                for(int i = 0; i < _size; ++i)
                {
                    temp[i] = vec._data[i];
                }

                delete [] _data;
                _data = temp;
                _size = vec._size;
                _capacity = vec._capacity;
                return *this;
            }

            void push_back(value_type val)
            {
                if(0 == _capacity)
                {
                    _capacity = 1;
                    _data = new value_type[1];
                }
                else if(_size+1 > _capacity)
                {
                    _capacity *= 2;
                    value_type* temp = new value_type[_capacity];
                    for(int i = 0; i < _size; ++i)
                    {
                        temp[i] = _data[i];
                    }
                    delete []_data;
                    _data = temp;
                }
                _data[_size] = val;
                ++_size;
            }

            void pop_back()
            {
                --_size;
            }

            size_t size()const
            {
                return _size;
            }

            size_t capacity()const
            {
                return _capacity;
            }

            bool empty()
            {
                return _size == 0;
            }

            value_type& operator[](size_t index)
            {
                return _data[index];
            }

            bool operator==(const Vector& vec)
            {
                if(_size != vec._size)
                {
                    return false;
                }
                for(int i = 0; i < _size; ++i)
                {
                    if(_data[i] != vec[i])
                    {
                        return false;
                    }
                }
                return true;
            }

            value_type front() const
            {
                return _data[0];
            }

            value_type back() const
            {
                return _data[_size-1];
            }
            //insert有问题
            void insert(iterator it, value_type val)
            {
                //求当前迭代器的位置与数据的开始位置相差的元素个数，即元素的下标
                int index = it - _data;
                if(0 == _capacity)
                {
                    _capacity = 1;
                    _data = new value_type[_capacity];
                    _data[0] = val;
                }
                //当数据的位置已经满了的时候，需要进行扩容
                else if(_size+1 > _capacity)
                {
                    _capacity *= 2;
                    value_type* temp = new value_type[_capacity];
                    for(int i = 0; i < _size; ++i)
                    {
                        temp[i] = _data[i];
                    }
                    temp[index] = val;
                    delete []_data;
                    _data = temp;
                }
                else
                {
                    _data[index] = val;
                }

                ++_size;
            }

            void erase(iterator it)
            {
                size_t index = it - _data;

                for(int i = index; i < _size - 1; ++i)
                {
                    _data[i] = _data[i+1];
                }
                --_size;
            }

            iterator begin()
            {
                return _data;
            }

            iterator end()
            {
                return _data + _size;
            }
    };
}

using namespace miniSTL;
int main()
    {
        Vector<char> vec;
        char* it = {};

        string s = "helloworld";
        for(int i = 0; i < s.size(); ++i)
        {
            vec.push_back(s[i]);
        }

        for(auto &x : vec)
        {
            cout << x << " ";
        }
        cout << endl;
        cout << vec.size() << endl;
        cout << vec.capacity() << endl;
        vec.pop_back();
        for(auto &x : vec)
        {
            cout << x;
        }        

        for(int i = 0; i < vec.size(); ++i)
        {
            cout << vec[i] << " ";
        }
        cout << endl;
        cout << vec.front() << endl;
        cout << vec.back() << endl;
        cout << vec.empty() << endl;
        vec.insert(it, 'd');
        for(int i = 0; i < vec.size(); ++i)
        {
            cout << vec[i] << " ";
        }
        return 0;
    }


```


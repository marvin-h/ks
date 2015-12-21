##内联命名空间

`inline namespace`，指示命名空间中的名称同时是外层命名空间直接包含的名称，可以用于命名空间的版本管理

例子：

```
namespace NS {
    inline namespace XX {}
}
```

c++98：

```
namespace Jim {
    namespace Basic {
        struct Knife { Knife() {} };
    }

    namespace Toolkit {
        template<typename T> class SwissArmyKnife {};
    }

    namespace Other {

    }

    using namespace Basic;
    using namespace Toolkit;
}

int main() {
    using namespace Jim;
    SwissArmyKnife<Knife> knife;
}
```

c++11：

```
namespace Jim {
    inline namespace Basic {
        struct Knife { Knife() {} };
    }

    inline namespace Toolkit {
        template<typename T> class SwissArmyKnife {};
    }

    namespace Other {

    }
}

int main() {
    using namespace Jim;
    SwissArmyKnife<Knife> knife;
}
```

命名空间版本控制：
用inline表示哪个命名空间是最新的

```
#include <iostream>
using namespace std;

namespace Jim {
    namespace V98 {
        struct Knife { Knife() { cout << "V98::Knife" << endl; } };
    }

    inline namespace V11 {
        struct Knife { Knife() { cout << "V11::Knife" << endl; } };
    }
}

int main() {
    using namespace Jim;
    Knife k; //V11::Knif
    V98::Knife k1; //V98::Knife
    V11::Knife k2; //V11::Knif
}
```
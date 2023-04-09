---
title: Ruby Exception Tree
slug: "/Ruby-Exception-Tree"
date: 2022-10-21
tags:
  - Ruby On Rails
---

1. Exception
    1. NoMemoryError
    2. ScriptError
        1. LoadError
        2. NotImplementedError
        3. SyntaxError
    3. SignalException
        1. Interrupt
    4. StandardError
        1. ArgumentError
        2. IOError
            1. EOFError
        3. IndexError
        4. LocalJumpError
        5. NameError
            1. NoMethodError
        6. RangeError
            1. FloatDomainError
        7. RegexpError
        8. RuntimeError
        9. SecurityError
        10. SystemCallError
        11. SystemStackError
        12. ThreadError
        13. TypeError
        14. ZeroDivisionError
    5. SystemExit
    6. fatal

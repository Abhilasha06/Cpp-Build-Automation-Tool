# Build-Automation-Tool

• Built in python, this tool is capable of exploring a given directory structure,
creating the action graph and then executing the action and its dependencies.

• Avoids duplication of work and performs independent action execution in
parallel whenever possible.

File Structure-

```
algorithms/
    build.json
    sort_bubble.cpp
    sort_merge.cpp
    sort_quick.cpp
build.json
test.cpp
```

```
algorithms/build.json
[
  {
    "name": "clean",
    "command": "rm -f *.o"
  },
  {
    "name": "sort_bubble",
    "command": "g++ -c sort_bubble.cpp"
  },
  {
    "name": "sort_merge",
    "command": "g++ -c sort_merge.cpp"
  },
  {
    "name": "sort_quick",
    "command": "g++ -c sort_quick.cpp"
  }
]
```

```
build.json
[
  {
    "name": "clean",
    "deps": ["algorithms/clean"],
    "command": "rm -f test.o && rm -f test_*.exe"
  },
  {
    "name": "test",
    "command": "g++ -std=c++11 -c test.cpp"
  },
  {
    "name": "test_sort_bubble",
    "deps": ["test", "algorithms/sort_bubble"],
    "command": "g++ test.o algorithms/sort_bubble.o -o test_sort_bubble.exe && ./test_sort_bubble.exe"
  },
  {
    "name": "test_sort_merge",
    "deps": ["test", "algorithms/sort_merge"],
    "command": "g++ test.o algorithms/sort_merge.o -o test_sort_merge.exe && ./test_sort_merge.exe"
  },
  {
    "name": "test_sort_quick",
    "deps": ["test", "algorithms/sort_quick"],
    "command": "g++ test.o algorithms/sort_quick.o -o test_sort_quick.exe && ./test_sort_quick.exe"
  },
  {
    "name": "test_all",
    "deps": ["test_sort_bubble", "test_sort_merge", "test_sort_quick"]
  }
]
```

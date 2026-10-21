
# Code Review Report — `game.cpp`

| Line Number | Defect Type | Why It Is a Problem | Proposed Solution | Severity |
|-------------|-------------|---------------------|-------------------|----------|
| 27, 31–33 | Uninitialized pointer array | `monsters[]` holds garbage pointers until assigned. | Initialize all pointers to `nullptr` in the constructor. | Low |
| 41, 119 | Array out-of-bounds / no capacity check | Six monsters are spawned into an array with capacity five. | Check capacity before insertion or use `std::vector`. | Critical |
| 47 | `=` instead of `==` | Assigns the ID instead of comparing it. | Use `if (monsters[i]->id == id)`. | Critical |
| 54–59, 123 | Missing null check | Dereferencing `nullptr` causes a crash. | Check whether the returned pointer is `nullptr`. | Critical |
| 55–56 | Signed/unsigned mixing | Unsigned subtraction can wrap around. | Use validated integer types and prevent negative damage. | High |
| 58 | Inconsistent variable use | Uses `dmg` in the check and `damage` in subtraction. | Use one validated variable and clamp health to zero. | Medium |
| 64 | Off-by-one loop | `i <= monsterCount` accesses an invalid index. | Change the condition to `i < monsterCount`. | High |
| 70–73 | Returns reference to local variable | The returned reference dangles after the local variable is destroyed. | Return `std::string` by value. | Critical |
| 71–72 | Missing null check | Accessing `m->id` can crash. | Check `m` before accessing its members. | High |
| 77 | Uninitialized variable | `sum` is used before initialization. | Initialize with `double sum = 0;`. | High |
| 80 | Division by zero / truncation | `monsterCount` may be zero and the result loses its fractional part. | Check for zero and return a `double`. | Medium |
| 84–85 | Missing null check | Accessing `m->name` may crash. | Check `m` before use. | High |
| 85–86 | Use after free | `m->name` is accessed after deletion. | Print the name before deleting the object. | Critical |
| 85 | Dangling pointer / double delete | The deleted pointer remains in the array and may be deleted again. | Null the slot, compact the array, and decrement the count. | Critical |
| 91 | Integer division | Fractional results are truncated and multiplication may overflow. | Use `/ 100.0` and validate the percentage. | Medium |
| 94–99 | Missing return on a path | Some execution paths return no value. | Add a return for every possible path. | High |
| 102, 105 | Buffer overflow | Long input can overflow `char name[10]`. | Use `std::string`. | Critical |
| 109 | Wrong deallocation | Memory allocated with `new[]` is freed using `delete`. | Use `delete[]` or replace the array with `std::string`. | High |
| 103, 107 | Uninitialized / unvalidated input | Failed input can leave health uninitialized; negative values are accepted. | Initialize health and validate input. | Medium |
| 108 | Unchecked capacity | The monster array may already be full. | Return and check a success status from `spawnMonster`. | Medium |
| 121 | Memory leak | `bonus` is allocated but never deleted. | Delete it or use `std::unique_ptr`. | Medium |
| 133 | Shallow copy / double delete | Copied objects share raw pointers and may delete the same monsters. | Implement deep copying or use smart pointers. | Critical |
| 12–15 | Public data members | External code can modify object state without validation. | Make members private and provide getters/setters. | Low |
| 17–22, 40 | Pass by value / no initializer list | Unnecessary string copies occur and members are assigned in the constructor body. | Use `const std::string&` and a constructor initializer list. | Low |

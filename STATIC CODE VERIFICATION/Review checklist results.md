Code Review Checklist
1. Initialization --- FAIL
- \(FAIL\) All local variables initialized before use? (L77 sum,
  L103 health)
- \(FAIL\) All class data members initialized in the constructor?
  (L27, L31--33 monsters[])
- \(FAIL\) Pointers set to nullptr when not yet in use? (L27)
- \(PASS\) Counter initialized correctly? (L32 monsterCount = 0)
2. Pointers (null / delete) --- FAIL
- \(FAIL\) Pointer checked for nullptr before dereference? (L56,
  L58, L59, L72, L86)
- \(FAIL\) Every new matched with a delete? (L121 bonus leaked)
- \(FAIL\) delete[] used for new[]? (L102 / L109)
- \(FAIL\) No access after delete? (L85--86)
- \(FAIL\) Pointer removed/nulled after delete? (L85)
- \(FAIL\) No double delete? (L37, L85, L133)
3. Arrays / Buffers --- FAIL
- \(FAIL\) Indexes within bounds? (L64--65)
- \(FAIL\) Capacity checked before insert? (L41, L119: 6 monsters into
  size 5)
- \(FAIL\) Input size limited to buffer size? (L102, L105)
- \(FAIL\) Deleted element removed from array? (L85)
4. Loops --- FAIL
- \(FAIL\) Loop bounds correct (no off-by-one)? (L64 <=)
- \(PASS\) Loops terminate correctly? (L36, L46, L78)
- \(PASS\) Loop conditions free of side effects? (L36, L46, L78)
5. Arithmetic --- FAIL
- \(FAIL\) No signed/unsigned mixing? (L55--56)
- \(FAIL\) Integer division avoided where fraction needed? (L91)
- \(FAIL\) Division by zero prevented? (L80)
- \(FAIL\) No overflow/truncation of results? (L80, L91)
- \(FAIL\) Input values validated? (L53--55, L107)
6. Control Flow --- FAIL
- \(FAIL\) Every non-void function returns on all paths? (L94--99
  playerRank)
- \(FAIL\) == used for comparison, not =? (L47)
- \(FAIL\) Conditions reachable and correct? (L56 never true)
- \(PASS\) All if / else if branches syntactically complete?
  (L95--98)
7. Function Calls --- FAIL
- \(FAIL\) Return values checked for null/error? (L54, L71, L84, L123)
- \(FAIL\) No reference/pointer returned to a local? (L70--73)
- \(FAIL\) Objects passed by const reference? (L17, L40)
- \(FAIL\) Argument types match parameters without unsafe conversion?
  (L55, L108)
- \(PASS\) Remaining calls use valid arguments? (L125--128)
8. Classes --- FAIL
- \(FAIL\) Rule of Three/Five followed for raw-memory ownership?
  (L25--88, L133)
- \(PASS\) Destructor frees owned objects? (L35--38)
- \(FAIL\) Data members encapsulated (private)? (L12--15)
- \(FAIL\) Constructor uses initializer list? (L17--22)
- \(FAIL\) Member functions keep object state consistent? (L83--87)
Final Result
  Category                 Result
  Initialization           Fail
  Pointers (null/delete)   Fail
  Arrays/Buffers           Fail
  Loops                    Fail
  Arithmetic               Fail
  Control Flow             Fail
  Function Calls           Fail
  Classes                  Fail

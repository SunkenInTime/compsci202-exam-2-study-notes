# Review log — concepts from Composer sessions

Short notes you can skim before the exam. Add new bullets here as we cover more.

---

## C++ pointers and syntax

- **Object vs pointer:** A `T` variable *is* the object (use `.member`). A `T*` holds *where* it lives (use `->member`, same as `(*p).member`).
- **`&x`:** address of `x` → gives a pointer when something needs `T*`.
- **`*p`:** the object `p` points to → go from pointer back to the thing.
- **`->`:** not “for structs only” — for **any pointer** to something with members (struct, class, union).

### Linked lists

- **`next`** is usually `Node*` → that’s the **link** (points elsewhere).
- **Data fields** (e.g. `value`) live **inside** the node → that’s the **payload**.
- Walk: `for (Node* cur = head; cur != nullptr; cur = cur->next)` — `cur->data` is the value, `cur->next` is the next pointer.

### Serialization

- Don’t rely on saving raw pointer **values** — addresses change each run.
- Save **values / order**, then **allocate new nodes** on load and **rewire** `next` pointers.

---

## `struct` vs `class` (C++)

- **Only default difference:** `struct` → members default to **public**; `class` → **private**.
- Otherwise the same (methods, inheritance, virtuals, etc.). Style: `struct` for simple bundles, `class` for encapsulation.

---

## `virtual`, override, and abstract

- **`virtual`** = dynamic dispatch: call through `Base*` / `Base&` uses the **actual object’s** type at runtime (vtable).
- **`virtual` with a body** = default implementation; derived classes **may** `override`.
- **Pure virtual** `virtual void f() = 0;` = **abstract** — base class usually can’t be instantiated; derived must implement (unless still abstract).
- **`virtual` ≠ “abstract”** — abstract is about **no** callable implementation in the base for that slot (`= 0`); virtual only controls **how** the call is resolved.

### Without `virtual` on the base

- **`Derived d; d.foo();`** or **`Derived* pd`** → can call **`Derived::foo`** if it exists.
- **`Base* pb = &derived; pb->foo();`** → **`Base::foo`** always — compiler uses **static type** of the pointer, not the dynamic type.
- Same name in derived **without** virtual base = often **hiding**, not polymorphic override.
- Use **`override`** on derived methods when the base is virtual — catches signature mistakes.

### Manual alternative to `virtual`

- **`dynamic_cast<Derived*>(basePtr)`** then call — same *idea* as polymorphism by hand; redundant for normal design but valid when you must branch on concrete type.

---

## OOP relationships

- **is-a:** inheritance (subtype is a kind of supertype).
- **has-a:** composition / **aggregation** — the whole is associated with parts (aggregation: parts often separable or shared; quiz wording often uses **has-a** for aggregation).

---

*Last updated: session covering pointers, struct/class, virtuality, is-a/has-a.*

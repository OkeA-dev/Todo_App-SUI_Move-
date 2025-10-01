# Todo App (SUI Move)

A decentralized todo list application built on the SUI blockchain using Move smart contracts. This project demonstrates fundamental Move concepts including object ownership, vector manipulation, and on-chain state management.

## 📋 Overview

The Todo List module allows users to create and manage their personal todo lists on the SUI blockchain. Each list is represented as an on-chain object that can be owned, transferred, and shared.

## ✨ Features

- **Create Todo Lists**: Initialize new todo lists as owned objects
- **Add Items**: Append new tasks to your list
- **Remove Items**: Delete completed tasks by index
- **Delete Lists**: Clean up and remove entire todo lists
- **Query Length**: Check the number of items in a list

## 🏗️ Smart Contract Structure

### Main Struct

```move
public struct TodoList has key, store {
    id: UID,
    items: vector<String>
}
```

The `TodoList` struct has two abilities:
- `key`: Can be used as a top-level object with a unique ID
- `store`: Can be stored inside other objects

### Public Functions

| Function | Description | Parameters | Returns |
|----------|-------------|------------|---------|
| `new()` | Creates a new empty todo list | `ctx: &mut TxContext` | `TodoList` |
| `add()` | Adds a new item to the list | `list: &mut TodoList, item: String` | None |
| `remove()` | Removes an item by index | `list: &mut TodoList, index: u64` | `String` |
| `delete()` | Deletes the entire list | `list: TodoList` | None |
| `length()` | Returns the number of items | `list: &TodoList` | `u64` |

## 🚀 Getting Started

### Prerequisites

- [SUI CLI](https://docs.sui.io/build/install) installed
- SUI wallet configured
- Basic understanding of Move language

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/Todo_App.git
cd Todo_App
```

2. Build the package:
```bash
sui move build
```

3. Run tests (if available):
```bash
sui move test
```

### Deployment

Deploy the module to SUI testnet:

```bash
sui client publish --gas-budget 100000000
```

Save the **Package ID** from the output for interactions.

## 💻 Usage Examples

### Creating a New Todo List

```bash
sui client call \
  --package <PACKAGE_ID> \
  --module todo_list \
  --function new \
  --gas-budget 10000000
```

### Adding an Item

```bash
sui client call \
  --package <PACKAGE_ID> \
  --module todo_list \
  --function add \
  --args <TODO_LIST_OBJECT_ID> "Buy groceries" \
  --gas-budget 10000000
```

### Removing an Item

```bash
sui client call \
  --package <PACKAGE_ID> \
  --module todo_list \
  --function remove \
  --args <TODO_LIST_OBJECT_ID> 0 \
  --gas-budget 10000000
```

### Deleting the List

```bash
sui client call \
  --package <PACKAGE_ID> \
  --module todo_list \
  --function delete \
  --args <TODO_LIST_OBJECT_ID> \
  --gas-budget 10000000
```

## 🔍 Key Concepts Demonstrated

### Object Ownership
Each `TodoList` is an owned object that belongs to the creator. The owner has full control over adding, removing, and deleting items.

### Vector Operations
The module uses SUI Move's vector type to store a dynamic list of todo items (strings).

### Object Deletion
Proper cleanup of objects by unpacking the struct and deleting the UID.

### Mutable References
Functions like `add()` and `remove()` take mutable references (`&mut`) to modify the list in place.

## 📂 Project Structure

```
Todo_App/
├── sources/
│   └── todo_list.move      # Main smart contract
├── tests/
│   └── todo_list_tests.move # Unit tests (optional)
├── Move.toml                # Package manifest
└── README.md                # This file
```

## 🧪 Testing

To add comprehensive tests, create a test module:

```move
#[test_only]
module todo_list::todo_list_tests {
    use todo_list::todo_list::{Self, TodoList};
    use std::string;
    
    #[test]
    fun test_create_and_add() {
        let ctx = tx_context::dummy();
        let list = todo_list::new(&mut ctx);
        
        todo_list::add(&mut list, string::utf8(b"Test item"));
        assert!(todo_list::length(&list) == 1, 0);
        
        todo_list::delete(list);
    }
}
```

## 🛠️ Future Enhancements

- [ ] Mark items as complete/incomplete
- [ ] Add timestamps to items
- [ ] Implement item priority levels
- [ ] Add sharing capabilities for collaborative lists
- [ ] Create events for list modifications
- [ ] Add item descriptions and metadata

## 📚 Resources

- [SUI Documentation](https://docs.sui.io/)
- [Move Language Book](https://move-language.github.io/move/)
- [SUI Move by Example](https://examples.sui.io/)

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

⭐ If you find this project helpful, please give it a star!

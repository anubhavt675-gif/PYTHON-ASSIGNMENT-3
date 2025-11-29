# Library Inventory Manager

Simple CLI-based library inventory manager built with Python.

## Features
- Add / Issue / Return books.
- Search by title and ISBN.
- Persistent storage in `data/catalog.json` (JSON).
- Robust exception handling and logging (`library.log`).
- Unit tests included.

## Run
1. Ensure Python 3.8+ is installed.
2. From project root run:
   ```bash
   python -m cli.main

---

# Explanations / line-by-line decisions (brief)

1. **Dataclass for Book** — `dataclasses` gives concise storage + `to_dict()` via `asdict()` for JSON persistence. Methods `issue`, `return_book`, `is_available` implement the required behavior.

2. **Inventory class** — keeps `List[Book]`, exposes add/search/display/issue/return. Uses `pathlib.Path` for robust file handling. `save_to_file()` writes atomically using `.tmp` then `replace()` to avoid corruption.

3. **JSON persistence & exception handling** — `load_from_file()` handles missing file (start empty) and catches `JSONDecodeError` to handle corrupted files. Logging is used for INFO and ERROR.

4. **CLI** — straightforward menu-driven loop with input validation, catches `KeyboardInterrupt` and other unexpected exceptions (logged). Saves on exit.

5. **Logging** — configured in `cli/main.py`. A `library.log` will be created in the project root. Use logging levels for important events.

6. **Unit tests** — `unittest` to cover basic add/search/issue/return flows. Uses a temporary file to avoid touching real data.

---

# How to run locally (quick)
1. Create the folders and files exactly as above.
2. From project root (folder containing `cli/`), run:
   ```bash
   python -m cli.main

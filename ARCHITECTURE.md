# Architecture

### Components
- CLI interface located in /bin/cli.js
- Unique item generator (/lib/generator.js): creates unique items with UUIDs and random unique content
- Storage module (/lib/storage.js): manages reading and writing items.jsonpersistent storage, with corruption handling and concurrency safety
- Search module (/lib/search.js): performs substring matching and case-insensitive searches over stored items
- Data file: /data/items.json, default location configurable by environment variable

### Folder Structure
/ek-unique-kuch-bnao-search-kro
  /bin
    cli.js             - CLI entry point parsing commands and calling library modules
  /lib
    generator.js       - UniqueItem creation logic
    storage.js         - Persistent storage with read/write, corruption handling
    search.js          - Search algorithm for stored items
  /data
    items.json         - Persistent JSON store of unique items
  /tests
    generator.test.js  - Tests for generator
    search.test.js     - Tests for search
    storage.test.js    - Tests for storage
  package.json
  README.md
  .gitignore
  .env.example

### Data Flow
User invokes CLI → CLI parses command → calls generator/storage/search modules → modules read/write /data/items.json → CLI outputs results or errors

### Key Decisions
- Node.js chosen for typical CLI environment
- UUID combined with random adjective-noun phrase as unique content
- JSON file for persistence
- Minimal dependencies: uuid for id generation
- Using built-in Node test runner
- Emphasis on reliability and graceful error handling in storage
- CLI commands correspond exactly to user needs: generate, search, list, delete, help

# DeBots

DeBot — is a smart contract facilitating conversation-like flow communication with a target smart contract. Instead of a usual smart contract, DeBots are executed locally. They work with target smart contracts providing a user interface to their functions. DeBot can work with one or many smart contracts, DeBots can also invoke each other, transparently to the user. DeBot prepares a message that it will send to a target smart contract (or smart contracts), but before it does it will emulate all the chain of transactions on a local user machine verifying and letting the user verify its correctness. DeBots are extremely powerful user technology, simplifying for the first time complicated interaction with a smart contract or systems of smart contracts.&#x20;

DeBots are completely decentralized by nature. They do not require any servers in between full nodes and a user device. There are no centralized or decentralized layers which clog user experience, like Web 3. Since DeBots run locally for all its phases, except for final message sending, they work much faster than any web or decentralized application. Using Pipes, DeBots can be presented to the user as a single action, interactive action flow, a form, a web page and so on (see below).

Users are interacting with DeBots via DeBot Browsers. Browsers contain the DeBot Engine (or DEngine) which takes care of running DeBots and providing D’Interfaces support.

D’Interfaces allows DeBots to receive input from users; query info about other smart contracts; query transactions and messages; receive data from external subsystems (like file system) and external devices (like NFC, camera and so on); call external function libraries that allow to do operations that are not supported by VM. For example, work with json, convert numbers to string and vice versa, encrypt/decrypt/sign data.

Every DeBot browser should strive to support D’Interface standards which are proposed, discussed and finalized in DeBot Interface Consortium (DeBot IS Consortium).

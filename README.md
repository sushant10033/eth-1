# Hotel Room Booking System

## Overview

The `HotelRoomBookingSystem` smart contract allows users to manage hotel room bookings on the Ethereum blockchain. It supports functionalities to add new rooms, book and vacate rooms, and check room availability. The contract ensures robust error handling and room state consistency through various mechanisms.

## Contract Structure

### Structs

- **Room**
  - `uint roomId`: Unique identifier for the room.
  - `string roomType`: Type of room (e.g., Single, Double, Suite).
  - `bool isBooked`: Indicates whether the room is currently booked.

### Mappings

- `mapping(uint => Room) public rooms`: Stores room details by room ID.
- `mapping(address => mapping(uint => bool)) public bookedRooms`: Tracks room bookings by user address and room ID.

### State Variables

- `uint public roomCount`: Tracks the total number of rooms added.

### Events

- `event RoomAdded(uint roomId, string roomType)`: Emitted when a new room is added.
- `event RoomBooked(address user, uint roomId)`: Emitted when a room is successfully booked.
- `event RoomVacated(address user, uint roomId)`: Emitted when a room is vacated.

### Functions

- **addRoom(string memory roomType) public**
  - Adds a new room to the system with a specified room type.
  - Emits `RoomAdded`.

- **bookRoom(uint roomId) public**
  - Books a specified room if it exists, is not already booked, and the user has not previously booked it.
  - Emits `RoomBooked`.

- **vacateRoom(uint roomId) public**
  - Vacates a room if it exists and the user has previously booked it.
  - Emits `RoomVacated`.

- **attemptBookRoom(uint roomId) public**
  - Attempts to book a room with error handling using `revert` statements.
  - Emits `RoomBooked` on successful booking.

- **checkRoomAvailability(uint roomId) public view returns (string memory roomType, bool isBooked)**
  - Returns the room type and booking status of the specified room.
  - Requires the room to exist.

- **internalCheck(uint roomId) internal view**
  - Internal function to ensure room state consistency using `assert`.

## Usage

1. **Add Rooms**: Call `addRoom` with the room type to add new rooms.
2. **Book Rooms**: Call `bookRoom` or `attemptBookRoom` with the room ID to book a room.
3. **Vacate Rooms**: Call `vacateRoom` with the room ID to vacate a booked room.
4. **Check Availability**: Call `checkRoomAvailability` with the room ID to check if the room is available and its type.

## Error Handling

- `require` statements are used for input validation and to enforce conditions.
- `revert` statements are used in `attemptBookRoom` for error handling.
- `assert` statements are used in `internalCheck` to ensure room state consistency.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.



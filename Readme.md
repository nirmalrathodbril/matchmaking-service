# Getting Started

This repository contains a Java backend application for a Chess Matchmaking Microservice, designed as a proof of concept (POC). The microservice enables players to register for a chess game, experience a waiting screen during opponent search, and receive match results within 30 seconds.

## Components

- **Player Registration Endpoint:**
  - REST endpoint for player registration.
- **Player Entity:**
  - Represents player details (playerId, skillLevel).
- **Player Service:**
  - Registers players and notifies the matchmaking system.
- **Matchmaking Consumer:**
  - Listens to the matchmaking queue and triggers matchmaking.
- **Matchmaking Service:**
  - Implements the matchmaking algorithm and notifies players.
- **Result Consumer:**
  - Listens to the result queue and processes match results.
- **RabbitMQ Configuration:**
  - Configuration for RabbitMQ queues.

## Installation

1. **Clone the Repository:**
    ```
    git clone https://github.com/your-username/chess-matchmaking-microservice.git
    ```

2. **Build and Run:**
    ```
    mvn clean install
    java -jar target/chess-matchmaking-microservice.jar
    ```

## Usage

- **Player Registration:**
  - Use the `/players/register` endpoint to register players.
- **Waiting Screen:**
  - Players will experience a waiting screen while the system searches for opponents.
- **Matchmaking Algorithm:**
  - Matchmaking is triggered automatically based on player registrations. The system will search for the opponent based on

## API
## Endpoint: `/join`

- **Method:** POST
- **Description:** Initiates the process for a player to join a game and starts the matchmaking process to find an opponent.
- **Request Body:**
  - Content-Type: `application/json`
  - Parameters:
    - `player` (JSON Object) - Represents player information containing `playerId` and `skillLevel`.
      - `playerId` (String) - Unique identifier for the player.
      - `skillLevel` (Integer) - Represents the skill level of the player.
- **Responses:**
  - **HTTP Status Code 200 OK:**
    - **Response Body:** JSON object representing the opponent player.
      - `playerId` (String) - Unique identifier of the opponent player.
      - `skillLevel` (Integer) - Skill level of the opponent player.
    - **Description:** Indicates successful joining of the game and provides opponent details for the player.
  - **HTTP Status Code 400 Bad Request:**
    - **Response Body:** Error message detailing the issue.
    - **Description:** Occurs when the request body is invalid or missing required parameters.
  - **HTTP Status Code 500 Internal Server Error:**
    - **Response Body:** Error message.
    - **Description:** Indicates an internal server error during the matchmaking process.

#### Sample Request:

```http
POST /join HTTP/1.1
Content-Type: application/json

{
  "playerId": "player123",
  "skillLevel": 8
}


Berry Blitz - Retro Avatar Adventure
Overview
Berry Blitz is a retro-style 2D survival game where players control an avatar that collects berries while avoiding obstacles and predators. The game features a canvas-based rendering system, touch/swipe controls for mobile, and progressive difficulty scaling. Players earn points by collecting different types of berries, each with unique scoring values and effects. The application is built as a full-stack TypeScript application with a React frontend and Express backend, though the current implementation primarily focuses on client-side game logic.

User Preferences
Preferred communication style: Simple, everyday language.

System Architecture
Frontend Architecture
Technology Stack:

React with TypeScript for UI components and game state management
Vite as the build tool and development server
Canvas API for game rendering
Tailwind CSS with Radix UI components for styling
Zustand for state management
Design Patterns:

Component-based architecture separating concerns (Home, Game, Statistics screens)
Custom game engine (GameEngine class) managing canvas rendering, collision detection, and game logic
Touch control system (TouchControls class) handling swipe gestures for mobile gameplay
State management through Zustand stores with middleware for persistence and subscriptions
Key Architectural Decisions:

Canvas-based rendering instead of DOM/React rendering for performance in game loops

Rationale: Canvas provides better performance for frequently updating game objects
Trade-off: More manual rendering code but smoother animations
Client-side game logic with no server persistence currently

Rationale: Simple arcade-style game doesn't require server-side validation
Future consideration: Backend could track leaderboards or user authentication
Mobile-first touch controls with desktop mouse support

Rationale: Primary target is mobile devices, but desktop testing is supported
Implementation: Swipe detection calculates direction from touch start/end positions
Local storage for statistics using Zustand persist middleware

Rationale: Player statistics (high scores, games played) survive page refreshes
Trade-off: Data is device-specific, not synced across devices
Backend Architecture
Technology Stack:

Express.js server with TypeScript
Drizzle ORM for database schema management
Neon serverless PostgreSQL database
Vite middleware integration for development
Design Patterns:

In-memory storage abstraction (IStorage interface) with future database migration path
Middleware-based request logging and error handling
Separation of concerns: routes, storage layer, and server setup
Key Architectural Decisions:

Storage abstraction layer with IStorage interface

Rationale: Allows switching from MemStorage (in-memory) to database implementation without changing application code
Current implementation: MemStorage class for development
Future path: Database-backed implementation using Drizzle ORM
Development/production separation with conditional Vite middleware

Rationale: Development uses Vite's HMR for fast iteration; production serves static assets
Implementation: Vite only initialized in development mode after route registration
Minimal API surface with routes prefixed by /api

Rationale: Game is primarily client-side; backend ready for future features
Future expansion: User authentication, leaderboards, game state persistence
Game Architecture
Core Systems:

Game Loop: RAF-based animation loop updating physics, rendering, and collision detection
Entity Management: Avatar, berries, obstacles, and predators with position/velocity tracking
Collision Detection: AABB (Axis-Aligned Bounding Box) collision between game objects
Progressive Difficulty: Predator speed increases with score; additional predators spawn over time
Power-up System: Time-based power-ups (speed boost, invincibility, freeze) affecting gameplay

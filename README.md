Ruby Chess Game ♔
A fully-featured command-line chess game implementation in Ruby with complete chess rules, move validation, check/checkmate detection, and save/load functionality.
Features

✨ Complete Chess Implementation - All standard chess pieces with proper movement rules
🎯 Move Validation - Prevents illegal moves and enforces chess rules
👑 Check & Checkmate Detection - Automatically detects check, checkmate, and stalemate
💾 Save/Load Games - Save your progress and resume games later
🤖 AI Player - Simple AI opponent that makes random legal moves
🎨 Visual Board Display - Unicode chess pieces with alternating square colors
⚡ Algebraic Notation - Standard chess notation (e2 e4, etc.)
🧪 Test Suite - Comprehensive RSpec tests included

Installation
Prerequisites

Ruby 2.7+ (recommended Ruby 3.0+)
No external gems required (uses only Ruby standard library)

Quick Start
bash# Clone or download the chess.rb file
# Run the game directly
ruby chess.rb
Usage
Starting a Game
bashruby chess.rb
Game Commands

Make a move: Enter moves in algebraic notation (e.g., e2 e4)
Save game: Type save to save the current game state
Load game: Type load to load a previously saved game
Quit: Type quit to exit the game

Move Notation
Use standard algebraic notation:

e2 e4 - Move piece from e2 to e4
g1 f3 - Move knight from g1 to f3
d1 h5 - Move queen from d1 to h5

Example Game Session
♔ Welcome to Chess! ♔
Enter moves as 'e2 e4' or 'quit' to exit, 'save' to save game

  a b c d e f g h
8 ♜ ♞ ♝ ♛ ♚ ♝ ♞ ♜ 8
7 ♟ ♟ ♟ ♟ ♟ ♟ ♟ ♟ 7
6 □ ■ □ ■ □ ■ □ ■ 6
5 ■ □ ■ □ ■ □ ■ □ 5
4 □ ■ □ ■ □ ■ □ ■ 4
3 ■ □ ■ □ ■ □ ■ □ 3
2 ♙ ♙ ♙ ♙ ♙ ♙ ♙ ♙ 2
1 ♖ ♘ ♗ ♕ ♔ ♗ ♘ ♖ 1
  a b c d e f g h

White's turn
> e2 e4
Game Architecture
Classes Overview
Core Classes

Piece - Base class for all chess pieces with common functionality
Board - Manages the 8x8 chess board and piece positions
Game - Handles game flow, player turns, and user interaction
AIPlayer - Simple AI that makes random legal moves

Piece Classes

Pawn - Implements pawn movement (forward, double-move, captures)
Rook - Implements rook movement (horizontal/vertical)
Knight - Implements knight movement (L-shaped moves)
Bishop - Implements bishop movement (diagonal)
Queen - Implements queen movement (combines rook + bishop)
King - Implements king movement (one square in any direction)

Key Features Implementation
Move Validation
rubydef valid_move?(from, to)
  piece = piece_at(from)
  return false unless piece
  return false unless in_bounds?(to)
  return false if piece.friendly?(piece_at(to))
  
  # Check if move would put own king in check
  !would_be_in_check?(piece.color, from, to)
end
Check Detection
rubydef in_check?(color)
  king = find_king(color)
  return false unless king
  
  enemy_color = color == :white ? :black : :white
  enemy_pieces = pieces_by_color(enemy_color)
  
  enemy_pieces.any? do |piece|
    piece.possible_moves.include?(king.position)
  end
end
Save/Load Functionality
rubydef save_game(filename = 'chess_save.json')
  save_data = {
    board: @board.to_json,
    current_player: @current_player
  }
  
  File.write(filename, save_data.to_json)
  puts "Game saved to #{filename}"
end
Testing
The game includes a comprehensive RSpec test suite covering:

Board functionality (piece placement, movement, bounds checking)
Piece movement validation
Game logic (move parsing, turn management)
Special chess rules (check, checkmate, stalemate)

Running Tests
bash# Install RSpec if not already installed
gem install rspec

# Run the test suite
rspec chess.rb
Test Coverage

Board Tests: Position validation, piece movement, bounds checking
Piece Tests: Movement patterns for all piece types
Game Tests: Move notation parsing, game state management
Integration Tests: Complete game scenarios

Game Rules Implemented
Standard Chess Rules

All pieces move according to standard chess rules
Pawns can move forward one or two squares on first move
Pawns capture diagonally
Castling is not yet implemented
En passant is not yet implemented
Pawn promotion is not yet implemented

Check & Checkmate

Automatic check detection
Players cannot make moves that put their own king in check
Checkmate detection ends the game
Stalemate detection results in a draw

Move Validation

Pieces cannot move to squares occupied by friendly pieces
Pieces cannot move through other pieces (except knights)
Moves are validated against piece-specific movement patterns

Extending the Game
Adding New Features
Castling Implementation:
rubydef can_castle?(king, rook)
  # Check if king and rook haven't moved
  # Check if path is clear
  # Check if king is not in check
end
Pawn Promotion:
rubydef promote_pawn(pawn, new_piece_type)
  # Replace pawn with chosen piece when reaching end rank
end
Enhanced AI:
rubyclass SmartAI < AIPlayer
  def evaluate_position
    # Implement position evaluation
  end
  
  def minimax(depth, maximizing_player)
    # Implement minimax algorithm
  end
end
File Structure
chess.rb                 # Main game file containing all classes
chess_save.json         # Generated save file (created when saving)
Contributing
Contributions are welcome! Areas for improvement:

Enhanced AI - Implement minimax algorithm or other AI strategies
Special Moves - Add castling, en passant, pawn promotion
GUI Version - Create a graphical interface
Network Play - Add multiplayer over network
Move History - Track and display move history
Game Analysis - Add position evaluation and move suggestions

Development Guidelines

Follow Ruby style conventions
Add tests for new features
Maintain backward compatibility
Document new methods and classes

Known Limitations

Castling is not implemented
En passant capture is not implemented
Pawn promotion is not implemented
AI is very basic (random moves only)
No move history or undo functionality
No time controls

License
This project is open source and available under the MIT License.
Acknowledgments

Unicode chess symbols for visual representation
Standard algebraic notation for move input
Object-oriented design principles for clean architecture


Enjoy your game of chess! ♔♕♖♗♘♙

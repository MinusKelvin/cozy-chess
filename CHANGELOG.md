# Changelog

## v0.3.4
### Added
- Added helper methods for handling UCI moves.
- Added `Square::relative_to` to get a square relative to some color.

## v0.3.3
### Added
- Added setters for the halfmove clock and fullmove number fields.

## v0.3.2
### Fixed
- Fixed bug where en passant was not correctly validated when parsing and building `Board`s.

## v0.3.1
### Fixed
- Fixed bug where `Board::is_legal` said castles while in check were legal.

## v0.3.0
### Added
- Added methods for obtaining Chess960 start positions from their Scharnagl number.
- Added PEXT bitboards using the BMI2 PEXT intrinsic. Potentially faster than the default algorithm. Enable using the `pext` feature. 
- Added `Board::hash_without_ep` method for fast equivalence checks excluding the en passant square.
- Added `Board::same_position` to check if two boards are equivalent under FIDE rules.
- Added `Board::colored_pieces`, a shorthand for `board.colors(color) & board.pieces(piece)`.
- Added `BitBoard::is_subset`, `BitBoard::is_superset`, and `BitBoard::is_disjoint`.

### Changed (**breaking**)
- `BitBoard`s now operate in a more set-wise manner instead of acting like a `u64`. Bit operators changed to match set operators.
- `BitBoard::popcnt` renamed to `BitBoard::len` for consistency with other data structures.
- `BoardBuilder`'s `fullmove_number` field changed to a `u16` for usability reasons.
- `Board`'s `FromStr` implementation now parses both FEN and Shredder FEN.

### Removed (**breaking**)
- `BitBoard` no longer implements `Iterator` directly.
- Sliding move functions are no longer `const` by default; Use the `const` variants if required.
- Unnecessary "try" variants on `Board` removed; The risk of panicking is accepted when `*_unchecked` methods are called.

### Fixed
- Overflow bug in `Square::try_offset` fixed.
- `FenParseError` is no longer unnameable.
- Fixed incorrect errors being returned in FEN parsing.
- Fixed some errors not being produced in FEN parsing.

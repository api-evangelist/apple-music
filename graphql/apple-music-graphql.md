# Apple Music GraphQL Schema

## Overview

This is a conceptual GraphQL schema for the Apple Music API (MusicKit API). The Apple Music API is a REST API provided by Apple through the Apple Developer Program. This schema represents the resources, relationships, and operations available via the API as GraphQL types and queries, enabling developers to reason about the data model in a graph-oriented way.

## Source API

- **Provider:** Apple Music (Apple Inc.)
- **API Name:** Apple Music API / MusicKit
- **Base URL:** `https://api.music.apple.com/v1`
- **Documentation:** https://developer.apple.com/documentation/applemusicapi
- **Authentication:** Apple Developer JWT (developer token); user library access requires a Music User Token (MusicKit)

## Schema Design Notes

The Apple Music API exposes a rich catalog of music resources (songs, albums, artists, music videos, playlists, stations) plus authenticated user library resources. The GraphQL schema mirrors this structure:

- **Catalog types** represent resources in the global Apple Music catalog (e.g., `Song`, `Album`, `Artist`, `MusicVideo`, `Playlist`, `Station`).
- **Library types** represent resources in the authenticated user's personal library (e.g., `LibrarySong`, `LibraryAlbum`, `LibraryArtist`, `LibraryPlaylist`, `LibraryMusicVideo`).
- **Relationship types** capture the associations between resources (e.g., `SongRelationships`, `AlbumSongs`, `ArtistAlbums`).
- **Attribute types** carry the data fields for each resource (e.g., `SongAttributes`, `AlbumAttributes`, `ArtistAttributes`).
- **Discovery types** model search, recommendations, charts, and recently-played (e.g., `Search`, `SearchResult`, `SearchHints`, `Recommendations`, `RecentlyPlayed`).
- **Auth/token types** model the authentication artifacts required by the API (`MusicKitToken`, `DeveloperToken`, `UserToken`, `APIKey`).
- **Storefront types** model the locale/region used for catalog lookups (`StoreFront`, `StoreFrontDetails`).

## Coverage

The schema covers 65 named GraphQL types spanning:

| Category | Types |
|---|---|
| Song | Song, SongDetails, SongAttributes, SongRelationships, SongArtists, SongAlbums, SongGenres |
| Album | Album, AlbumDetails, AlbumAttributes, AlbumSongs, AlbumArtwork |
| Artist | Artist, ArtistDetails, ArtistAttributes, ArtistAlbums, ArtistSongs, ArtistPlaylists, ArtistGenres, ArtistBio |
| Artwork | Artwork, ArtworkDetails, ArtworkURL |
| Genre | Genre, GenreDetails, GenreName |
| Playlist | Playlist, PlaylistDetails, PlaylistAttributes, PlaylistTracks, PlaylistArtwork |
| Library | LibraryPlaylist, LibrarySong, LibraryAlbum, LibraryArtist, LibraryMusicVideo, LibrarySongPlayback |
| Station/Radio | Station, RadioStation, AppleMusicStation, BeatsStation, UserStation |
| Social/Activity | SocialActivity, RecentlyPlayed, Recommendations, PersonalMix, PersonalStation |
| Search | Search, SearchResult, SearchHints, CatalogSearch, LibrarySearch |
| StoreFront | StoreFront, StoreFrontDetails |
| Music Video | MusicVideo, MusicVideoDetails |
| Curator | Curator, CuratorPlaylist |
| Auth | MusicKitToken, DeveloperToken, UserToken, APIKey |

## Usage

This schema is conceptual. To use the Apple Music API:

1. Enroll in the Apple Developer Program.
2. Create a MusicKit identifier and private key in the Apple Developer portal.
3. Generate a signed JWT developer token (valid up to 6 months).
4. For user library access, obtain a Music User Token via MusicKit JS or native MusicKit frameworks.
5. Call `https://api.music.apple.com/v1` endpoints with the `Authorization: Bearer <developer-token>` header and, for library routes, the `Music-User-Token` header.

## References

- Apple Music API Reference: https://developer.apple.com/documentation/applemusicapi
- MusicKit JS: https://developer.apple.com/documentation/musickitjs
- MusicKit (native): https://developer.apple.com/documentation/musickit
- Getting Tokens: https://developer.apple.com/documentation/applemusicapi/getting_keys_and_creating_tokens

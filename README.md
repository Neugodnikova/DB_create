# DB_create
--создание таблицы Жанры
create table if not exists Genre(
	id serial primary key,
	title varchar(60) not null
);

--создание таблицы Исполнители
create table if not exists Artist(
	id serial primary key,
	nick_name varchar(120) not null
);


--создание таблицы ЖанрыИсполнители
-- ключ Многие ко многим
CREATE TABLE IF NOT EXISTS GenreArtist (
	genre_id INTEGER REFERENCES Genre(id),
	artist_id INTEGER REFERENCES Artist(id),
	CONSTRAINT pk PRIMARY KEY (genre_id, artist_id)
);

--создание таблицы Альбом
create table if not exists Album(
	id serial primary key,
	title varchar(360) not null,
	year_create date	
);

--создание таблицы ИсполнителиАльбом
-- ключ Многие ко многим
CREATE TABLE IF NOT EXISTS ArtistAlbum (
	album_id INTEGER REFERENCES Album(id),
	artist_id INTEGER REFERENCES Artist(id),
	CONSTRAINT pk1 PRIMARY KEY (album_id, artist_id)
);

--создание таблицы Трек
create table if not exists Song(
	--id serial not null,
	title varchar(360) not null,
	year_create date,
	song_id INTEGER PRIMARY KEY REFERENCES Album(id)
);

--создание таблицы Сборник
create table if not exists Mix(
	id serial primary key,
	title varchar(360) not null,
	year_create date
);

--создание таблицы ТрекиСборник
-- ключ Многие ко многим
CREATE TABLE IF NOT EXISTS SongMix (
	mix_id INTEGER REFERENCES Mix(id),
	song_id INTEGER REFERENCES Song(album_id),
	CONSTRAINT pk2 PRIMARY KEY (song_id, mix_id)
);

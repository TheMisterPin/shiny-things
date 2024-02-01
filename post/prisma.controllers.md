# Prisma Controllers and Relationships Guide 🛠️

This guide explains how to create controllers for managing database operations using Prisma, focusing on adding objects with relationships and retrieving data with various techniques.

## Table of Contents

- [Prisma Controllers and Relationships Guide 🛠️](#prisma-controllers-and-relationships-guide-️)
  - [Table of Contents](#table-of-contents)
  - [Adding Data with Relationships](#adding-data-with-relationships)
    - [Creating a Movie Controller 🎬](#creating-a-movie-controller-)
- [Prisma Controllers and Relationships Guide 🛠️](#prisma-controllers-and-relationships-guide-️-1)
  - [Table of Contents](#table-of-contents-1)
  - [Adding Data with Relationships](#adding-data-with-relationships-1)
    - [Creating a Movie Controller 🎬](#creating-a-movie-controller--1)
  - [Initializing Relationships 🧩](#initializing-relationships-)
  - [Data Retrieval Techniques](#data-retrieval-techniques)
  - [Field Exclusion/Inclusion 🛠️](#field-exclusioninclusion-️)
    - [Exclude Fields Example](#exclude-fields-example)
    - [Include Fields Example](#include-fields-example)
  - [Handling One-to-Many Relationships 🌳](#handling-one-to-many-relationships-)
  - [Field Exclusion/Inclusion 🛠️](#field-exclusioninclusion-️-1)
    - [Exclude Fields Example](#exclude-fields-example-1)
    - [Include Fields Example](#include-fields-example-1)
    - [Handling One-to-Many Relationships 🌳](#handling-one-to-many-relationships--1)
  - [Implementing Pagination 📄](#implementing-pagination-)

## Adding Data with Relationships

### Creating a Movie Controller 🎬

A movie controller manages operations related to movie entities in the database, such as adding, updating, and deleting movies.

```typescript
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

async function addMovie(data) {
  return await prisma.movie.create({
    data,
  });
}
```

Back to Top

Initializing Relationships 🧩
To establish relationships when adding new records, use methods like connectOrCreate to link related entities.

Example: Adding a Movie with Genre 🎥

```typescript
Copy code
async function addMovieWithGenre(movieTitle, genreName) {
  return await prisma.movie.create({
    data: {
      title: movieTitle,
      genre: {
        connectOrCreate: {
          where: { name: genreName },
          create: { name: genreName },
        },
      },
    },
  });
}

// Usage
addMovieWithGenre('Inception', 'Sci-Fi').then(movie => {
  console.log('Added movie:', movie);
});
```

Back to Top

Data Retrieval Techniques
Retrieving with Parameters 🔍
Filter data retrieval by specific parameters to refine your queries.

```typescript
Copy code
async function getMoviesByTitle(title: string) {
  return await prisma.movie.findMany({
    where: { title },
  });
}
```

# Prisma Controllers and Relationships Guide 🛠️

This guide explains how to create controllers for managing database operations using Prisma, focusing on adding objects with relationships and retrieving data with various techniques.

## Table of Contents

- [Prisma Controllers and Relationships Guide 🛠️](#prisma-controllers-and-relationships-guide-️)
  - [Table of Contents](#table-of-contents)
  - [Adding Data with Relationships](#adding-data-with-relationships)
    - [Creating a Movie Controller 🎬](#creating-a-movie-controller-)
- [Prisma Controllers and Relationships Guide 🛠️](#prisma-controllers-and-relationships-guide-️-1)
  - [Table of Contents](#table-of-contents-1)
  - [Adding Data with Relationships](#adding-data-with-relationships-1)
    - [Creating a Movie Controller 🎬](#creating-a-movie-controller--1)
  - [Initializing Relationships 🧩](#initializing-relationships-)
  - [Data Retrieval Techniques](#data-retrieval-techniques)
  - [Field Exclusion/Inclusion 🛠️](#field-exclusioninclusion-️)
    - [Exclude Fields Example](#exclude-fields-example)
    - [Include Fields Example](#include-fields-example)
  - [Handling One-to-Many Relationships 🌳](#handling-one-to-many-relationships-)
  - [Field Exclusion/Inclusion 🛠️](#field-exclusioninclusion-️-1)
    - [Exclude Fields Example](#exclude-fields-example-1)
    - [Include Fields Example](#include-fields-example-1)
    - [Handling One-to-Many Relationships 🌳](#handling-one-to-many-relationships--1)
  - [Implementing Pagination 📄](#implementing-pagination-)


## Adding Data with Relationships

### Creating a Movie Controller 🎬

A movie controller manages operations related to movie entities in the database, such as adding, updating, and deleting movies.

```typescript
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

async function addMovie(data) {
  return await prisma.movie.create({
    data,
  });
}
```

Back to Top

## Initializing Relationships 🧩
To establish relationships when adding new records, use methods like connectOrCreate to link related entities.

Example: Adding a Movie with Genre 🎥

```typescript
Copy code
async function addMovieWithGenre(movieTitle, genreName) {
  return await prisma.movie.create({
    data: {
      title: movieTitle,
      genre: {
        connectOrCreate: {
          where: { name: genreName },
          create: { name: genreName },
        },
      },
    },
  });
}

// Usage
addMovieWithGenre('Inception', 'Sci-Fi').then(movie => {
  console.log('Added movie:', movie);
});
```

Back to Top

## Data Retrieval Techniques
Retrieving with Parameters 🔍
Filter data retrieval by specific parameters to refine your queries.

```typescript
Copy code
async function getMoviesByTitle(title: string) {
  return await prisma.movie.findMany({
    where: { title },
  });
}
```



## Field Exclusion/Inclusion 🛠️
Control the shape of returned data by specifying which fields to include or exclude.

### Exclude Fields Example
```typescript
Copy code
async function getMovieDetailsExcludingCreatedAt(movieId: string) {
  return await prisma.movie.findUnique({
    where: { id: movieId },
    select: {
      title: true,
      overview: true,
      genre: true,
      createdAt: false,
    },
  });
}
```

### Include Fields Example

```typescript
Copy code
async function getMovieDetailsIncludingSpecificFields(movieId: string) {
  return await prisma.movie.findUnique({
    where: { id: movieId },
    select: {
      title: true,
      overview: true,
      genre: true,
    },
  });
}
```

## Handling One-to-Many Relationships 🌳
Retrieve related entities in one-to-many relationships efficiently.

```typescript
Copy code
async function getGenreWithMovies(genreId: string) {
  return await prisma.genre.findUnique({
    where: { id: genreId },
    include: { movies: true },
  });
}
```




## Field Exclusion/Inclusion 🛠️
Control the shape of returned data by specifying which fields to include or exclude.

### Exclude Fields Example

```typescript
Copy code
async function getMovieDetailsExcludingCreatedAt(movieId: string) {
  return await prisma.movie.findUnique({
    where: { id: movieId },
    select: {
      title: true,
      overview: true,
      genre: true,
      createdAt: false,
    },
  });
}
```

### Include Fields Example

```typescript
Copy code
async function getMovieDetailsIncludingSpecificFields(movieId: string) {
  return await prisma.movie.findUnique({
    where: { id: movieId },
    select: {
      title: true,
      overview: true,
      genre: true,
    },
  });
}
```


### Handling One-to-Many Relationships 🌳
Retrieve related entities in one-to-many relationships efficiently.

```typescript
Copy code
async function getGenreWithMovies(genreId: string) {
  return await prisma.genre.findUnique({
    where: { id: genreId },
    include: { movies: true },
  });
}
```

Back to Top

## Implementing Pagination 📄
Use pagination to manage large datasets, specifying how many records to fetch and how many to skip.

```typescript
Copy code
async function getMoviesPaginated(page: number, pageSize: number = 10) {
  return await prisma.movie.findMany({
    take: pageSize,
    skip: (page - 1) * pageSize,
  });
}
```
---
<div align="right">
[Using Data](axios.md)
</div>

<div align="left">
  [Back to top](#table-of-contents)
</div>
<div align="center">
  [Back Home](../README.md)
</div>
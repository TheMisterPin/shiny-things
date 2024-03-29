# Prisma📘
-[Prisma Controllers](prisma.controllers.md)
## Table of Contents

- [Prisma📘](#prisma)
  - [Table of Contents](#table-of-contents)
    - [What is Prisma? 🌟](#what-is-prisma-)
    - [Prisma Schema 📄](#prisma-schema-)
      - [Schema](#schema)
    - [One-to-One Relationships 🧩](#one-to-one-relationships-)
    - [One-to-Many Relationships 🌳](#one-to-many-relationships-)
    - [Many-to-Many Relationships 🌐](#many-to-many-relationships-)
    - [Handling One-to-Many in MongoDB without Native Support 🛠️](#handling-one-to-many-in-mongodb-without-native-support-️)

### What is Prisma? 🌟

Prisma is an open-source database toolkit that includes an ORM (Object-Relational Mapping) for Node.js and TypeScript...

### Prisma Schema 📄

#### Schema

```prisma
// Define your models here
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  profile   Profile?
  // ... other fields
}

model Profile {
  id     Int    @id @default(autoincrement())
  bio    String
  userId Int    @unique
  user   User   @relation(fields: [userId], references: [id])
  // ... other fields
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String?
  authorId  Int
  author    User     @relation(fields: [authorId], references: [id])
  // ... other fields
}
// ... other models
```

### One-to-One Relationships 🧩

🌐 In a one-to-one relationship, a record in one model is linked to only one record in another model. For example, in the schema above, each User has one Profile, and each Profile is associated with one User.

### One-to-Many Relationships 🌳

🚀 A one-to-many relationship occurs when a record in one model can be related to many records in another model. For example, a single User can have many Posts.

### Many-to-Many Relationships 🌐

💫 In a many-to-many relationship, records in one model can be linked to multiple records in another model and vice versa. This is often implemented using arrays of ObjectIDs in both models in MongoDB. For instance, Users can have a list of favorite Movies, and each Movie can have a list of Users who favorited it.

### Handling One-to-Many in MongoDB without Native Support 🛠️

- 🌟 **Embedding Documents**: Embed the related documents directly within a single document. This is efficient but can lead to data duplication.
- 📚 **Referencing Documents**: Store the IDs of the related documents. This is similar to how relationships are handled in SQL databases.

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

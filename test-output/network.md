```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-vswezr@email.com",
    "username": "author-vswezr",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-vswezr@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci12c3dlenIiLCJpYXQiOjE1Nzg5NTQ0MDEsImV4cCI6MTU3OTEyNzIwMX0.GRUbUWZVuh_Up1FURNMvL2iJYZlWyCowmGqTyCDtFIY",
    "username": "author-vswezr",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-w6kokp@email.com",
    "username": "authoress-w6kokp",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-w6kokp@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy13Nmtva3AiLCJpYXQiOjE1Nzg5NTQ0MDEsImV4cCI6MTU3OTEyNzIwMX0.yTEBBkTFI6eBmynAnj3F39fMF8oBvSEUag-ab82Vw2w",
    "username": "authoress-w6kokp",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-u8htg4@email.com",
    "username": "non-author-u8htg4",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-u8htg4@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItdThodGc0IiwiaWF0IjoxNTc4OTU0NDAxLCJleHAiOjE1NzkxMjcyMDF9.MjrGSQSZjKc1Uhuma5EO4V25m1zSGwMT_AGWS-u7FHg",
    "username": "non-author-u8htg4",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ld040g",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954401824,
    "updatedAt": 1578954401824,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-wo2x5x",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954401854,
    "updatedAt": 1578954401854,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-ld040g
```
```
200 OK

{
  "article": {
    "createdAt": 1578954401824,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-ld040g",
    "updatedAt": 1578954401824,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-wo2x5x
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1578954401854,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-wo2x5x",
    "updatedAt": 1578954401854,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/o2pmoc
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [o2pmoc]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-wo2x5x

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1578954401854,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-wo2x5x",
    "updatedAt": 1578954401854,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-wo2x5x

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1578954401854,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-wo2x5x",
    "updatedAt": 1578954401854,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-wo2x5x

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1578954401854,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-wo2x5x",
    "updatedAt": 1578954401854,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-wo2x5x

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-wo2x5x

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-wo2x5x

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-wo2x5x

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-wo2x5x]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-wo2x5x

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-vswezr]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-ld040g/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1578954401824,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-ld040g",
    "updatedAt": 1578954401824,
    "favoritedBy": [
      "non-author-u8htg4"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-ld040g
```
```
200 OK

{
  "article": {
    "createdAt": 1578954401824,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-ld040g",
    "updatedAt": 1578954401824,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-ld040g/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-ld040g_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-ld040g_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-ld040g/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1578954401824,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-ld040g",
    "updatedAt": 1578954401824,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-ld040g
```
```
200 OK

{}
```
```
GET /articles/title-ld040g
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-ld040g]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-wo2x5x
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-vswezr]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "w8i7vv",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-nnf4t3",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954402906,
    "updatedAt": 1578954402906,
    "author": {
      "username": "authoress-w6kokp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "w8i7vv",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "6t9bd8",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-onbfgg",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954402943,
    "updatedAt": 1578954402943,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "6t9bd8",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "bur5hz",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-7b9j1q",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954402971,
    "updatedAt": 1578954402971,
    "author": {
      "username": "authoress-w6kokp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "bur5hz",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "r7k3rz",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-6wj1rs",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954402996,
    "updatedAt": 1578954402996,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "r7k3rz",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "x1mq0m",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-dyfnrp",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403018,
    "updatedAt": 1578954403018,
    "author": {
      "username": "authoress-w6kokp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "x1mq0m",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "v7s01t",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-314k5h",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403041,
    "updatedAt": 1578954403041,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "v7s01t",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "nej1s",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-vs666c",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403065,
    "updatedAt": 1578954403065,
    "author": {
      "username": "authoress-w6kokp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "nej1s",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "fkcct9",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mithyf",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403086,
    "updatedAt": 1578954403086,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "fkcct9",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "bi7034",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-33ior3",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403108,
    "updatedAt": 1578954403108,
    "author": {
      "username": "authoress-w6kokp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "bi7034",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "5p6gqh",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-8cdd73",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403130,
    "updatedAt": 1578954403130,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "5p6gqh",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "99urg5",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-83ur3g",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403153,
    "updatedAt": 1578954403153,
    "author": {
      "username": "authoress-w6kokp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "99urg5",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "pz3r15",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-wedcs4",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403175,
    "updatedAt": 1578954403175,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "pz3r15",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "h2bthb",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-v6cdg2",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403196,
    "updatedAt": 1578954403196,
    "author": {
      "username": "authoress-w6kokp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "h2bthb",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "lvw4r7",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-34xli4",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403232,
    "updatedAt": 1578954403232,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "lvw4r7",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "324oru",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ntlgz",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403255,
    "updatedAt": 1578954403255,
    "author": {
      "username": "authoress-w6kokp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "324oru",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "da5dab",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-tty14k",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403279,
    "updatedAt": 1578954403279,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "da5dab",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "2ldydl",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-8x73bj",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403304,
    "updatedAt": 1578954403304,
    "author": {
      "username": "authoress-w6kokp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "2ldydl",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "-z6c32j",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-jf90d2",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403329,
    "updatedAt": 1578954403329,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "-z6c32j",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "wwqyl3",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-5cjueq",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403357,
    "updatedAt": 1578954403357,
    "author": {
      "username": "authoress-w6kokp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "wwqyl3",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "hjyu1o",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-wnr1bl",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954403398,
    "updatedAt": 1578954403398,
    "author": {
      "username": "author-vswezr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "hjyu1o",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "hjyu1o",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403398,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wnr1bl",
      "updatedAt": 1578954403398,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "wwqyl3"
      ],
      "createdAt": 1578954403357,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5cjueq",
      "updatedAt": 1578954403357,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "-z6c32j",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403329,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jf90d2",
      "updatedAt": 1578954403329,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2ldydl",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403304,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8x73bj",
      "updatedAt": 1578954403304,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "da5dab",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403279,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tty14k",
      "updatedAt": 1578954403279,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "324oru",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403255,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ntlgz",
      "updatedAt": 1578954403255,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lvw4r7",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403232,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-34xli4",
      "updatedAt": 1578954403232,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h2bthb",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403196,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v6cdg2",
      "updatedAt": 1578954403196,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "pz3r15",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403175,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wedcs4",
      "updatedAt": 1578954403175,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "99urg5",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403153,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-83ur3g",
      "updatedAt": 1578954403153,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5p6gqh",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403130,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8cdd73",
      "updatedAt": 1578954403130,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bi7034",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403108,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-33ior3",
      "updatedAt": 1578954403108,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fkcct9",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403086,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mithyf",
      "updatedAt": 1578954403086,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nej1s",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403065,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vs666c",
      "updatedAt": 1578954403065,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "v7s01t"
      ],
      "createdAt": 1578954403041,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-314k5h",
      "updatedAt": 1578954403041,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "x1mq0m"
      ],
      "createdAt": 1578954403018,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dyfnrp",
      "updatedAt": 1578954403018,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r7k3rz",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954402996,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6wj1rs",
      "updatedAt": 1578954402996,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bur5hz",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954402971,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7b9j1q",
      "updatedAt": 1578954402971,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6t9bd8",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954402943,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-onbfgg",
      "updatedAt": 1578954402943,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w8i7vv"
      ],
      "createdAt": 1578954402906,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nnf4t3",
      "updatedAt": 1578954402906,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "fkcct9",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403086,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mithyf",
      "updatedAt": 1578954403086,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "-z6c32j",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403329,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jf90d2",
      "updatedAt": 1578954403329,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "324oru",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403255,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ntlgz",
      "updatedAt": 1578954403255,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "pz3r15",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403175,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wedcs4",
      "updatedAt": 1578954403175,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bi7034",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403108,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-33ior3",
      "updatedAt": 1578954403108,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "v7s01t"
      ],
      "createdAt": 1578954403041,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-314k5h",
      "updatedAt": 1578954403041,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bur5hz",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954402971,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7b9j1q",
      "updatedAt": 1578954402971,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-w6kokp
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "wwqyl3"
      ],
      "createdAt": 1578954403357,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5cjueq",
      "updatedAt": 1578954403357,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2ldydl",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403304,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8x73bj",
      "updatedAt": 1578954403304,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "324oru",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403255,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ntlgz",
      "updatedAt": 1578954403255,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h2bthb",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403196,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v6cdg2",
      "updatedAt": 1578954403196,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "99urg5",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403153,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-83ur3g",
      "updatedAt": 1578954403153,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bi7034",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403108,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-33ior3",
      "updatedAt": 1578954403108,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nej1s",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403065,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vs666c",
      "updatedAt": 1578954403065,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "x1mq0m"
      ],
      "createdAt": 1578954403018,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dyfnrp",
      "updatedAt": 1578954403018,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bur5hz",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954402971,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7b9j1q",
      "updatedAt": 1578954402971,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w8i7vv"
      ],
      "createdAt": 1578954402906,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nnf4t3",
      "updatedAt": 1578954402906,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-u8htg4
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-vswezr&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "hjyu1o",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403398,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wnr1bl",
      "updatedAt": 1578954403398,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "-z6c32j",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403329,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jf90d2",
      "updatedAt": 1578954403329,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-vswezr&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "da5dab",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403279,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tty14k",
      "updatedAt": 1578954403279,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lvw4r7",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403232,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-34xli4",
      "updatedAt": 1578954403232,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "hjyu1o",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403398,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wnr1bl",
      "updatedAt": 1578954403398,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "wwqyl3"
      ],
      "createdAt": 1578954403357,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5cjueq",
      "updatedAt": 1578954403357,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "-z6c32j",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403329,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jf90d2",
      "updatedAt": 1578954403329,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2ldydl",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403304,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8x73bj",
      "updatedAt": 1578954403304,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "da5dab",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403279,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tty14k",
      "updatedAt": 1578954403279,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "324oru",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403255,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ntlgz",
      "updatedAt": 1578954403255,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lvw4r7",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403232,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-34xli4",
      "updatedAt": 1578954403232,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h2bthb",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403196,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v6cdg2",
      "updatedAt": 1578954403196,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "pz3r15",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403175,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wedcs4",
      "updatedAt": 1578954403175,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "99urg5",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403153,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-83ur3g",
      "updatedAt": 1578954403153,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5p6gqh",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403130,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8cdd73",
      "updatedAt": 1578954403130,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bi7034",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403108,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-33ior3",
      "updatedAt": 1578954403108,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fkcct9",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403086,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mithyf",
      "updatedAt": 1578954403086,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nej1s",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403065,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vs666c",
      "updatedAt": 1578954403065,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "v7s01t"
      ],
      "createdAt": 1578954403041,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-314k5h",
      "updatedAt": 1578954403041,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "x1mq0m"
      ],
      "createdAt": 1578954403018,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dyfnrp",
      "updatedAt": 1578954403018,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r7k3rz",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954402996,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6wj1rs",
      "updatedAt": 1578954402996,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bur5hz",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954402971,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7b9j1q",
      "updatedAt": 1578954402971,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6t9bd8",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954402943,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-onbfgg",
      "updatedAt": 1578954402943,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w8i7vv"
      ],
      "createdAt": 1578954402906,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nnf4t3",
      "updatedAt": 1578954402906,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-w6kokp/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-w6kokp",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "wwqyl3"
      ],
      "createdAt": 1578954403357,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5cjueq",
      "updatedAt": 1578954403357,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2ldydl",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403304,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8x73bj",
      "updatedAt": 1578954403304,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "324oru",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403255,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ntlgz",
      "updatedAt": 1578954403255,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h2bthb",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403196,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v6cdg2",
      "updatedAt": 1578954403196,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "99urg5",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403153,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-83ur3g",
      "updatedAt": 1578954403153,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bi7034",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403108,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-33ior3",
      "updatedAt": 1578954403108,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nej1s",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403065,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vs666c",
      "updatedAt": 1578954403065,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "x1mq0m"
      ],
      "createdAt": 1578954403018,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dyfnrp",
      "updatedAt": 1578954403018,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bur5hz",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954402971,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7b9j1q",
      "updatedAt": 1578954402971,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w8i7vv"
      ],
      "createdAt": 1578954402906,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nnf4t3",
      "updatedAt": 1578954402906,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-vswezr/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-vswezr",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "hjyu1o",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403398,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wnr1bl",
      "updatedAt": 1578954403398,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "wwqyl3"
      ],
      "createdAt": 1578954403357,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5cjueq",
      "updatedAt": 1578954403357,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "-z6c32j",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403329,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jf90d2",
      "updatedAt": 1578954403329,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2ldydl",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403304,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8x73bj",
      "updatedAt": 1578954403304,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "da5dab",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403279,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tty14k",
      "updatedAt": 1578954403279,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "324oru",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403255,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ntlgz",
      "updatedAt": 1578954403255,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lvw4r7",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403232,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-34xli4",
      "updatedAt": 1578954403232,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h2bthb",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403196,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v6cdg2",
      "updatedAt": 1578954403196,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "pz3r15",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403175,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wedcs4",
      "updatedAt": 1578954403175,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "99urg5",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403153,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-83ur3g",
      "updatedAt": 1578954403153,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5p6gqh",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403130,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8cdd73",
      "updatedAt": 1578954403130,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bi7034",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954403108,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-33ior3",
      "updatedAt": 1578954403108,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fkcct9",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954403086,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mithyf",
      "updatedAt": 1578954403086,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nej1s",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954403065,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vs666c",
      "updatedAt": 1578954403065,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "v7s01t"
      ],
      "createdAt": 1578954403041,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-314k5h",
      "updatedAt": 1578954403041,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "x1mq0m"
      ],
      "createdAt": 1578954403018,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dyfnrp",
      "updatedAt": 1578954403018,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r7k3rz",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1578954402996,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6wj1rs",
      "updatedAt": 1578954402996,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bur5hz",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1578954402971,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7b9j1q",
      "updatedAt": 1578954402971,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6t9bd8",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1578954402943,
      "author": {
        "username": "author-vswezr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-onbfgg",
      "updatedAt": 1578954402943,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w8i7vv"
      ],
      "createdAt": 1578954402906,
      "author": {
        "username": "authoress-w6kokp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nnf4t3",
      "updatedAt": 1578954402906,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "2ldydl",
    "tag_16",
    "tag_mod_2_0",
    "tag_mod_3_1",
    "6t9bd8",
    "tag_1",
    "tag_mod_2_1",
    "nej1s",
    "tag_6",
    "tag_mod_3_0",
    "da5dab",
    "tag_15",
    "pz3r15",
    "tag_11",
    "tag_mod_3_2",
    "bur5hz",
    "tag_2",
    "h2bthb",
    "tag_12",
    "-z6c32j",
    "tag_17",
    "tag_0",
    "w8i7vv",
    "324oru",
    "tag_14",
    "lvw4r7",
    "tag_13",
    "tag_5",
    "v7s01t",
    "fkcct9",
    "tag_7",
    "tag_4",
    "x1mq0m",
    "5p6gqh",
    "tag_9",
    "tag_18",
    "wwqyl3",
    "tag_a",
    "tag_b",
    "99urg5",
    "tag_10",
    "hjyu1o",
    "tag_19",
    "bi7034",
    "tag_8",
    "r7k3rz",
    "tag_3"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-he89d2@email.com",
    "username": "author-he89d2",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-he89d2@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1oZTg5ZDIiLCJpYXQiOjE1Nzg5NTQ0MDQsImV4cCI6MTU3OTEyNzIwNH0.xhaWfBNXOLfts9UIksC6dHdHwO0LCyeKKf9c2buGsBY",
    "username": "author-he89d2",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-rt9eq2@email.com",
    "username": "commenter-rt9eq2",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-rt9eq2@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci1ydDllcTIiLCJpYXQiOjE1Nzg5NTQ0MDQsImV4cCI6MTU3OTEyNzIwNH0.ec3_phf0LQEYez52ZOf24ETcDUUiwWrKBsA9Mei5_f8",
    "username": "commenter-rt9eq2",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-dv31of",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1578954404712,
    "updatedAt": 1578954404712,
    "author": {
      "username": "author-he89d2",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-dv31of/comments

{
  "comment": {
    "body": "test comment tyhlca"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "3bbc14d6-7a32-4442-95d9-77155c51488a",
    "slug": "title-dv31of",
    "body": "test comment tyhlca",
    "createdAt": 1578954404790,
    "updatedAt": 1578954404790,
    "author": {
      "username": "commenter-rt9eq2",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-dv31of/comments

{
  "comment": {
    "body": "test comment ehf4o0"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "0b74bb0c-5cd0-4018-88fb-dd49ede008d1",
    "slug": "title-dv31of",
    "body": "test comment ehf4o0",
    "createdAt": 1578954404819,
    "updatedAt": 1578954404819,
    "author": {
      "username": "commenter-rt9eq2",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-dv31of/comments

{
  "comment": {
    "body": "test comment hb6ohg"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "b3c5b851-84fe-4139-aa2f-2d18e9ce5dbf",
    "slug": "title-dv31of",
    "body": "test comment hb6ohg",
    "createdAt": 1578954404849,
    "updatedAt": 1578954404849,
    "author": {
      "username": "commenter-rt9eq2",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-dv31of/comments

{
  "comment": {
    "body": "test comment xzb8c1"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "a40776bc-2641-4b70-ac3c-95a9c5b2c3d1",
    "slug": "title-dv31of",
    "body": "test comment xzb8c1",
    "createdAt": 1578954404875,
    "updatedAt": 1578954404875,
    "author": {
      "username": "commenter-rt9eq2",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-dv31of/comments

{
  "comment": {
    "body": "test comment gtw7un"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "be354e94-5707-421e-8086-156ca5669cd1",
    "slug": "title-dv31of",
    "body": "test comment gtw7un",
    "createdAt": 1578954404904,
    "updatedAt": 1578954404904,
    "author": {
      "username": "commenter-rt9eq2",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-dv31of/comments

{
  "comment": {
    "body": "test comment avyz44"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "5232fcdc-7994-4383-87a2-91ca29bc9ecb",
    "slug": "title-dv31of",
    "body": "test comment avyz44",
    "createdAt": 1578954404928,
    "updatedAt": 1578954404928,
    "author": {
      "username": "commenter-rt9eq2",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-dv31of/comments

{
  "comment": {
    "body": "test comment lnned1"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "87007c13-21b2-4193-9e83-11759ff63580",
    "slug": "title-dv31of",
    "body": "test comment lnned1",
    "createdAt": 1578954404960,
    "updatedAt": 1578954404960,
    "author": {
      "username": "commenter-rt9eq2",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-dv31of/comments

{
  "comment": {
    "body": "test comment r09dzz"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "ac9162f3-d4d9-4531-b3b4-ce3eb9f6ddad",
    "slug": "title-dv31of",
    "body": "test comment r09dzz",
    "createdAt": 1578954404984,
    "updatedAt": 1578954404984,
    "author": {
      "username": "commenter-rt9eq2",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-dv31of/comments

{
  "comment": {
    "body": "test comment rbwx4u"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "7806af37-3ab6-4a12-9edb-92991905a97f",
    "slug": "title-dv31of",
    "body": "test comment rbwx4u",
    "createdAt": 1578954405013,
    "updatedAt": 1578954405013,
    "author": {
      "username": "commenter-rt9eq2",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-dv31of/comments

{
  "comment": {
    "body": "test comment gwt80g"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "63793f5d-3832-4a26-af09-333867ed7d3b",
    "slug": "title-dv31of",
    "body": "test comment gwt80g",
    "createdAt": 1578954405043,
    "updatedAt": 1578954405043,
    "author": {
      "username": "commenter-rt9eq2",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-dv31of/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-dv31of/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment j3bliy"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-dv31of/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1578954404984,
      "id": "ac9162f3-d4d9-4531-b3b4-ce3eb9f6ddad",
      "body": "test comment r09dzz",
      "slug": "title-dv31of",
      "author": {
        "username": "commenter-rt9eq2",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1578954404984
    },
    {
      "createdAt": 1578954404790,
      "id": "3bbc14d6-7a32-4442-95d9-77155c51488a",
      "body": "test comment tyhlca",
      "slug": "title-dv31of",
      "author": {
        "username": "commenter-rt9eq2",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1578954404790
    },
    {
      "createdAt": 1578954405043,
      "id": "63793f5d-3832-4a26-af09-333867ed7d3b",
      "body": "test comment gwt80g",
      "slug": "title-dv31of",
      "author": {
        "username": "commenter-rt9eq2",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1578954405043
    },
    {
      "createdAt": 1578954405013,
      "id": "7806af37-3ab6-4a12-9edb-92991905a97f",
      "body": "test comment rbwx4u",
      "slug": "title-dv31of",
      "author": {
        "username": "commenter-rt9eq2",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1578954405013
    },
    {
      "createdAt": 1578954404904,
      "id": "be354e94-5707-421e-8086-156ca5669cd1",
      "body": "test comment gtw7un",
      "slug": "title-dv31of",
      "author": {
        "username": "commenter-rt9eq2",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1578954404904
    },
    {
      "createdAt": 1578954404819,
      "id": "0b74bb0c-5cd0-4018-88fb-dd49ede008d1",
      "body": "test comment ehf4o0",
      "slug": "title-dv31of",
      "author": {
        "username": "commenter-rt9eq2",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1578954404819
    },
    {
      "createdAt": 1578954404960,
      "id": "87007c13-21b2-4193-9e83-11759ff63580",
      "body": "test comment lnned1",
      "slug": "title-dv31of",
      "author": {
        "username": "commenter-rt9eq2",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1578954404960
    },
    {
      "createdAt": 1578954404875,
      "id": "a40776bc-2641-4b70-ac3c-95a9c5b2c3d1",
      "body": "test comment xzb8c1",
      "slug": "title-dv31of",
      "author": {
        "username": "commenter-rt9eq2",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1578954404875
    },
    {
      "createdAt": 1578954404928,
      "id": "5232fcdc-7994-4383-87a2-91ca29bc9ecb",
      "body": "test comment avyz44",
      "slug": "title-dv31of",
      "author": {
        "username": "commenter-rt9eq2",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1578954404928
    },
    {
      "createdAt": 1578954404849,
      "id": "b3c5b851-84fe-4139-aa2f-2d18e9ce5dbf",
      "body": "test comment hb6ohg",
      "slug": "title-dv31of",
      "author": {
        "username": "commenter-rt9eq2",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1578954404849
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-dv31of/comments/3bbc14d6-7a32-4442-95d9-77155c51488a
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-dv31of/comments/0b74bb0c-5cd0-4018-88fb-dd49ede008d1
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-rt9eq2]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-dv31of/comments/0b74bb0c-5cd0-4018-88fb-dd49ede008d1
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-dv31of/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.9jmymyv0kua@email.com",
    "username": "user1-0.9jmymyv0kua",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.9jmymyv0kua@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOWpteW15djBrdWEiLCJpYXQiOjE1Nzg5NTQ0MDUsImV4cCI6MTU3OTEyNzIwNX0.rTPuqGkAtLguC2MD9Z62K_Wtfe-m3qe7c6NhWQC8UJU",
    "username": "user1-0.9jmymyv0kua",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.9jmymyv0kua@email.com",
    "username": "user1-0.9jmymyv0kua",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.9jmymyv0kua]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.9jmymyv0kua@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.9jmymyv0kua@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.9jmymyv0kua@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.9jmymyv0kua@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOWpteW15djBrdWEiLCJpYXQiOjE1Nzg5NTQ0MDUsImV4cCI6MTU3OTEyNzIwNX0.rTPuqGkAtLguC2MD9Z62K_Wtfe-m3qe7c6NhWQC8UJU",
    "username": "user1-0.9jmymyv0kua",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.sby9j9z4amp",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.sby9j9z4amp]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.9jmymyv0kua@email.com",
    "password": "0.a7y31jr3sjq"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.9jmymyv0kua@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOWpteW15djBrdWEiLCJpYXQiOjE1Nzg5NTQ0MDUsImV4cCI6MTU3OTEyNzIwNX0.rTPuqGkAtLguC2MD9Z62K_Wtfe-m3qe7c6NhWQC8UJU",
    "username": "user1-0.9jmymyv0kua",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.9jmymyv0kua
```
```
200 OK

{
  "profile": {
    "username": "user1-0.9jmymyv0kua",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.5axb7jclcq5
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.5axb7jclcq5]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1Nzg5NTQ0MDUsImV4cCI6MTU3OTEyNzIwNX0.4KxEhYOsN0LiZ-8z2AnBpXxSJwyifqEgyZN5LRnI7XQ",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.yula6xhpylf",
    "email": "user2-0.yula6xhpylf@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.yula6xhpylf@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAueXVsYTZ4aHB5bGYiLCJpYXQiOjE1Nzg5NTQ0MDUsImV4cCI6MTU3OTEyNzIwNX0.tLorGOUCvmiq050NRBHHXzuAg10n4lUBVlivblDyh7U",
    "username": "user2-0.yula6xhpylf",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.9jmymyv0kua@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.9jmymyv0kua",
    "email": "updated-user1-0.9jmymyv0kua@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOWpteW15djBrdWEiLCJpYXQiOjE1Nzg5NTQ0MDUsImV4cCI6MTU3OTEyNzIwNX0.rTPuqGkAtLguC2MD9Z62K_Wtfe-m3qe7c6NhWQC8UJU"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.9jmymyv0kua",
    "email": "updated-user1-0.9jmymyv0kua@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOWpteW15djBrdWEiLCJpYXQiOjE1Nzg5NTQ0MDUsImV4cCI6MTU3OTEyNzIwNX0.rTPuqGkAtLguC2MD9Z62K_Wtfe-m3qe7c6NhWQC8UJU"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.9jmymyv0kua",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOWpteW15djBrdWEiLCJpYXQiOjE1Nzg5NTQ0MDUsImV4cCI6MTU3OTEyNzIwNX0.rTPuqGkAtLguC2MD9Z62K_Wtfe-m3qe7c6NhWQC8UJU"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.9jmymyv0kua",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOWpteW15djBrdWEiLCJpYXQiOjE1Nzg5NTQ0MDUsImV4cCI6MTU3OTEyNzIwNX0.rTPuqGkAtLguC2MD9Z62K_Wtfe-m3qe7c6NhWQC8UJU"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.2ple093g5u6@email.com",
    "username": "user2-0.2ple093g5u6",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.2ple093g5u6@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuMnBsZTA5M2c1dTYiLCJpYXQiOjE1Nzg5NTQ0MDUsImV4cCI6MTU3OTEyNzIwNX0.u6DgtC5W9jjDVY-q9enr2pRRlW3Mp_w3hQAr1kS2eis",
    "username": "user2-0.2ple093g5u6",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.2ple093g5u6@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.2ple093g5u6@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2020-01-13T22:26:45.939Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```

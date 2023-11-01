# towers
A Kotlin framework that allows you to build web applications with soft layers that are not limited in abstraction level

This is POC.

Configuration of your application `App.kt` will be looks like: 

```kotlin
App {
  RoutingLayer {
    sockets {
      User {
        withTower {
          tower {
            first(JsonUsers::class)
              .next(WebValidated::class)
          }
        }
      }
      Post {
        withTower {
          tower {
            first(XmlPosts::class)
          }
        }
      }
    }
  }
  BusinessLauer {
    sockets {
      User {
        withTower {
          tower {
            first(SimpleUsers::class)
              .next(WithPostHistory::class)
          }
        }
      }
      Post {
        withTower {
          tower {
            first(SimplePosts::class)
              .next(RenderedAsMarkdown::class)
          }
        }
      }
    }
  }
  SourceLayer {
    sockets {
      User {
        withTower {
          tower {
            first(PgUsers::class)
              .next(ValidatedUsers::class)
              .next(TransactionalUsers::class)
              .next(CachingUsers::class)
          }
        }
      }
      Post {
        wihtTower {
          tower {
            first(GhPosts::class)
              .next(CachedPosts::class)
          }
        }
      }
    }
  }
}
```

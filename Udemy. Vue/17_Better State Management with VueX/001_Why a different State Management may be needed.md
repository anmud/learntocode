# Why a different State Management may be needed

Previously we see how to use the `event bus` to transport `data` between different parts of the application. But for big applications this might not be the best tool. For large applications we really might want a different setup, when we have a central place where we store everything, but also some specific places where we define our ways to change the `data`, to get the `data`, so that we have a clear separation of concerns and can for easily track when we made each change and so on. `VueX` offers us such a pattern 
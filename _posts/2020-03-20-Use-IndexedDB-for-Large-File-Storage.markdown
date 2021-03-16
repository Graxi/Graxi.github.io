---
layout: default
title: 'Using IndexedDB for large file storage'
categories: [Visualization]
permalink: /visualization/large-file-storage-solution-in-browser
comments: true
---

When I worked on a project for real-time monitoring in IoT, I did an interesting feature. Since it’s impossible for the maintenance staff to stare at the screen day and night, they hope to record the real-time data into the database and revisit historical files another day. My responsibility is to create such an interface to upload a number of files and then visualize them.

#### Why not LocalStorage

It’s no wonder that we will have to store those files in the browser after upload. As being told, each file should contain the data stream of half an hour at a frequency of once per second and users should be able to upload a number of them. So what’s the storage option?

Speaking of storing data in the browser, the first option that jumps into my mind is certainly LocalStorage. But it doesn’t suit for this specific use case for three reasons:

- It’s said that LocalStorage has a size limit up to 5MB which is much lower than what are requested to save
- Storing data in LocalStorage happens in the main thread and may block the UI if the process takes long
- The file data may be messed up with the state of the app if you have already used LocalStorage to persist state(which is exactly my case)

#### IndexedDB Comes to Rescue

With concerns above, I decided to try with indexedDB and it turned out to be a very wise decision. Compared to LocalStorage, it has advantages as below:

- IndexedDB has a higher size limit because the storage space is based on your hard drive size
- Storing data in IndexedDB is a asynchronous process and will not block applications
- It’s a different storage mechanism from LocalStorage and totally separated from app state management
IndexedDB is also available in Web Workers

I recommend using localForage library for storage operations like reading and writing. The API is very straightforward and easy to understand.


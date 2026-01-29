can read from a json
can write to a json

# implementing custom ordering into file.gallery

currently, file.gallery has no way of knowing how files should be ordered semantically. the current implementation organizes them alphanumerically which works for formal compositions but in natural compositions results in a dom order that is nonsensical (reword this). 

taking inspiration from ds_store

garden_store will allow file.gallery to remember the semantic order of files while not affecting how they are rendered. it should also enable things like
- custom sorting per directory through a sort-method property
- potential optimizations for only updating items if they have moved or only replanting index.html's if the directory has been updated (file.gallery likely does not need this kind of optimization, but it would be possible!)

check if the file exists in garden_store
1. when processing a directory, make a new array for each index in garden_store.json
2. for each file in processedfiles, iterate through garden_store's files array with each index stored in the new array
3. if it does, update the file at its index and then remove the index from the stored indexes array. if it does not exist, push it to the end of garden_store's files.
4. at the end, if there are any indexes left in the stored index array, remove the items at those indexes from garden_store's files (as they are no longer in the directory or have been added to gardenignore)
5. update the index.html, iterating through the order of files in garden_store

# gardenconfig

make features opt-in only

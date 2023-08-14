# Order
Ordered source code makes finding stuff faster

## File
1. Imports
2. Combined Types (`type Handler<T> = `...)
3. Supporting small classes (`class PreviewAngle`, bigger classes into own file)
4. Main exported Class (`export class AngleComponent`)
5. Default subclasses/implementations (`export class HashRouter`)

## General Classes
1. Constants (`readonly animationDuration = 2000;`)
2. Events & Observables (`onPriceUpdate: (price: number) => void;`)
3. Variables (`animationState: number;`)
4. Constructor
5. Public methods
6. Private methods

## Components
1. Parent / Parameters (`declare parent: RingEditComponent`)
2. Constants
3. Events & Observables (`onPriceUpdate: (price: number) => void;`)
4. Referenced elements (`canvas: HTMLCanvasElement`)
5. Variables
6. Constructor
7. `onload`
8. `onunload`
9. `render`
10. Sub-renders (`renderGalleryItem(item: RingViewModel) ...`)
11. Public methods
12. Private helpers

## Services
Fist main (`getBook`) then different types (`getAuthors`) if a service (`BookService`) contains handlers multiple types

1. Get multiple (`getBooks`, `getFeaturedBooks`)
2. Get single (`getBook`)
3. Create (`publishBook`)
4. Update (`publishBookRevision`)
5. Delete (`redactBook`)
7. Private helpers (`generateBookCoverThumbnail`)
# VideoItem

A layout item that displays a video.

A layout item that displays a video. Items can be accessed or created from a `Form`. `VideoItem` allows developers to embed YouTube videos in forms with customizable properties including title, help text, video URL, alignment, and width.

## Methods

### duplicate()
`duplicate(): VideoItem`

Creates a copy of this item and appends it to the end of the form.

### getAlignment()
`getAlignment(): Alignment`

Gets the video's horizontal alignment.

### getHelpText()
`getHelpText(): String`

Gets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s).

### getId()
`getId(): Integer`

Gets the item's unique identifier.

### getIndex()
`getIndex(): Integer`

Gets the index of the item among all the items in the form.

### getTitle()
`getTitle(): String`

Gets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).

### getType()
`getType(): ItemType`

Gets the item's type, represented as an `ItemType`.

### getWidth()
`getWidth(): Integer`

Gets the video's width in pixels.

### setAlignment(alignment)
`setAlignment(alignment: Alignment): VideoItem`

Sets the video's horizontal alignment.

### setHelpText(text)
`setHelpText(text: String): VideoItem`

Sets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s).

### setTitle(title)
`setTitle(title: String): VideoItem`

Sets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).

### setVideoUrl(youtubeUrl)
`setVideoUrl(youtubeUrl: String): VideoItem`

Sets the video itself from a given YouTube URL or YouTube video ID.

### setWidth(width)
`setWidth(width: Integer): VideoItem`

Sets the video's width in pixels. Only the video's width can be set. Height is set automatically to maintain the video's proportions.

# DeafVSR Dataset Release

This repository accompanies the release of the deafVSR dataset, created to support research in personalized visual speech recognition for Deaf individuals. The dataset focuses on visual speech captured from Deaf signers and is intended to help develop and evaluate models that account for person-specific speech patterns.

## Dataset structure

This release contains the metadata files below. The video clips are identified by their source path and YouTube video ID in the CSV files.

```text
deafvsr/
├── README.md
├── deaf_df.csv          # Clips from Deaf speakers
└── accented_df.csv      # Clips from accented speakers
```

The `video_path` column describes the intended location of each extracted clip. The media files are not included in this metadata release; they can be obtained from the source YouTube videos using the `video_id`, `start`, and `end` columns, subject to the availability and terms of each source video.

## CSV format

Both CSV files use the following columns:

| Column | Description |
| --- | --- |
| `video_path` | Relative path and filename of the extracted clip. |
| `video_name` | Name of the extracted clip. |
| `video_id` | YouTube video ID of the source video. |
| `status` | Annotation or processing status for the clip. |
| `start` | Clip start time in seconds in the source video. |
| `end` | Clip end time in seconds in the source video. |
| `transcript` | Original transcript for the clip. |
| `processed_text` | Normalized transcript used for processing or evaluation. |
| `num_words` | Number of words in `processed_text`. |
| `num_seconds` | Duration of the clip in seconds. |

## Downloading the source clips

For a row in either CSV, construct the source URL as:

```text
https://www.youtube.com/watch?v=<video_id>
```

For example, a row with `video_id=ABC123`, `start=21.5`, and `end=35.9` refers to the segment from 21.5 to 35.9 seconds of `https://www.youtube.com/watch?v=ABC123`.

One way to download and extract a clip is:

```bash
yt-dlp -f 'bv*[ext=mp4]+ba[ext=m4a]/b[ext=mp4]' \
	-o source.mp4 'https://www.youtube.com/watch?v=<video_id>'
ffmpeg -i source.mp4 -ss <start> -to <end> -c copy clip.mp4
```

Replace `<video_id>`, `<start>`, and `<end>` with values from the CSV row. The resulting clip can be stored at the location specified by `video_path`. Some sources may be unavailable or may have usage restrictions, so access and redistribution must be checked before downloading or sharing them.

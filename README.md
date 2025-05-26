# IStoreQueryService/Query/v1

This is a Steam Web API endpoint that is **not officially documented, this is only what i tested and know how it works**. You can test it yourself [here](https://steamapi.xpaw.me/#IStoreQueryService/Query).

<hr>

Returns filtered store data for up to 1000 apps per request.

```http
  GET https://api.steampowered.com/IStoreQueryService/Query/v1/?key={KEY}&input_json={INPUT_JSON}
```

| Param        | Type     | Description                        |
| :----------- | :------- | :--------------------------------- |
| `key`        | `string` | A Steam Web API Key. **Required**  |
| `input_json` | `string` | **URI encoded** json. **Required** |

<br>

#### `input_json`:

```json
{
    "query": {},
    "context": {},
    "data_request": {}
}
```

<br>

-   **"query"**:

| Property | Type     | Description                                                 |
| -------- | -------- | ----------------------------------------------------------- |
| `start`  | `number` | From which item index the response begins, use as pagination.     |
| `count`  | `number` | Max of items to return (default: 10, max: 1000).            |
| `sort`   | `number` | An id for sorting. Tells the response how to sort the data. |
| `filter` | `object` | An object with filter configuration.                        |

<br>

`sort`:

-   **1** - Alphabetical order.
-   **2** - Ascending `appid`.
-   **20** - Most recent.
-   **21** - Percentage of positive reviews (desc).

<br>

`filter`:

| Property               | Type       | Description                                            |
| ---------------------- | ---------- | ------------------------------------------------------ |
| `released_only`        | `boolean`  | Return only released apps.                             |
| `coming_soon_only`     | `boolean`  | Return only coming soon apps.                          |
| `type_filters`         | `object`   | Which app types to return.                             |
| `tagids_must_match`    | `object[]` | Return only apps that contains the specified tag ids.  |
| `tagids_exclude`       | `number[]` | Don't return apps that contains the specified tag ids. |
| `global_top_n_sellers` | `number`   | Return only apps in the top "n" most selled.           |

<br>

`type_filters`:

-   "include_apps" `boolean`
-   "include_packages" `boolean`
-   "include_bundles" `boolean`
-   "include_games" `boolean`
-   "include_demos" `boolean`
-   "include_mods" `boolean`
-   "include_dlc" `boolean`
-   "include_software" `boolean`
-   "include_video" `boolean`
-   "include_hardware" `boolean`
-   "include_series" `boolean`
-   "include_music" `boolean`

<br>

`tagids_must_match`:

To specify the tag ids you must pass in objects with the `tagids` array. Each `tagids` can only include 1 tag id, to specify multiple tags you need to pass in multiple objects with `tagids`.

```json
"tagids_must_match": [{"tagids": ["1628"]}, {"tagids": ["1664"]}]
```

<br>

-   **"context"**:

| Property       | Type     | Description                                                                                      |
| -------------- | -------- | ------------------------------------------------------------------------------------------------ |
| `elanguage`    | `number` | An ID for the language that the data will be returned in (if avaiable). Defaults to 0 (english). |
| `country_code` | `string` | e.g. 'US', 'FR', 'DE', 'BR'. Which country to pull data from. **Required**                       |

> `country_code`doesn't seem to affect data like reviews or price.

<br>

- **"data_request":**

**Required** for item data to be included, if not set, only `appids` will be returned.

| Property                       | Type      | Description                                                     |
| ------------------------------ | --------- | --------------------------------------------------------------- |
| `include_assets`               | `boolean` |                                                                 |
| `include_release`              | `boolean` |                                                                 |
| `include_platforms`            | `boolean` |                                                                 |
| `include_all_purchase_options` | `boolean` |                                                                 |
| `include_screenshots`          | `boolean` |                                                                 |
| `include_trailers`             | `boolean` |                                                                 |
| `include_ratings`              | `boolean` |                                                                 |
| `include_tag_count`            | `number`  | How many tags to include, if not set, no tags will be returned. |
| `include_reviews`              | `boolean` |                                                                 |
| `include_basic_info`           | `boolean` |                                                                 |
| `include_supported_languages`  | `boolean` |                                                                 |
| `include_full_description`     | `boolean` |                                                                 |
| `include_included_items`       | `boolean` |                                                                 |
| `include_links`                | `boolean` |                                                                 |

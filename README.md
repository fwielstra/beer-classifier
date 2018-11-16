Get 10 media images for a given beer ID (depends on [jq](https://stedolan.github.io/jq)); run this in the folder you want the images to show up:

    curl "https://api.untappd.com/v4/beer/info/5860?client_id=$CLIENT_ID&client_secret=$CLIENT_SECRET"

    curl "https://api.untappd.com/v4/beer/info/1977303?client_id=E773E0DCBDDE1C8496E180A8BA6E2D2569EEE2B8&client_secret=8F26F2C81FFAEF932E3EE53FBB2FDBA77796FD81" | jq '.response.beer.media.items[].photo.photo_img_lg' | xargs -n1 curl -O

Alternatively, to avoid hitting the 100 / hour api limit, write curl output to a json file and work from there:

    curl "https://api.untappd.com/v4/beer/info/5860?client_id=$CLIENT_ID&client_secret=$CLIENT_SECRET" > images.json
    cat images.json | jq '.response.beer.media.items[].photo.photo_img_lg' | xargs -n1 curl -O

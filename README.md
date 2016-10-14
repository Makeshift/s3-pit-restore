# S3 point in time restore

This is the repository for s3-pit-restore, a point in time restore tool
for Amazon S3.

The typical scenario in which you may need this tool is when you have
enabled versioning on an S3 bucket and want to restore some or all of
the files to a certain point in time.

Doing this with the web interface is time consuming: Amazon S3 web management
gui doesn't offer a simple way to do that on a massive scale.

With this tool you can easly restore a repository to a point in time
with a simple command like this:

`:~$ s3-pit-restore -b my-bucket -d my-restored-bucket -t "06-17-2016 23:59:50 +2"`

Choosing the correct time and date to restore at is simply a matter of getting
that information clicking the *Versions: Show* button from the S3 web gui
and navigating through the, now appeared, versions timestamps. 

## Installing

With pip install:

`:~# pip3 install s3-pit-restore`

or clone the repository and launch:

`:~# python3 setup.py install`

## Howto

`s3-pit-restore` can do a lot of interesting things. The base one is restoring an entire bucket to a previous state:

`:~# s3-pit-restore -b my-bucket -d my-restored-bucket -t "06-17-2016 23:59:50 +2"`

Another thing it can do is to restore a subfolder (*prefix*) of a bucket:

`:~# s3-pit-restore -b my-bucket -d my-restored-subfolder -p mysubfolder -t "06-17-2016 23:59:50 +2"`

You can also speedup the download if you have bandwidth using more parallel workers:

`:~# s3-pit-restore -b my-bucket -d my-restored-subfolder -p mysubfolder -t "06-17-2016 23:59:50 +2" --max-workers 100`

If want to restore a well definided time stamp, you can use a starting and ending timestamp (a month in this example):

`:~# s3-pit-restore -b my-bucket -d my-restored-subfolder -p mysubfolder -f "05-01-2016 00:00:00 +2" -t "06-01-2016 00:00:00 +2"`

## Testing

s3-pit-restore comes with a testing suite. You can run it with:

`./s3-pit-restore -b my-bucket -d /tmp/ --test`

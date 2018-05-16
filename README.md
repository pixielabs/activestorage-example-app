# Active Storage Example App

A sample Rails application using
[activestorage](http://edgeguides.rubyonrails.org/active_storage_overview.html)
for file storage and upload.

#### Running the app

Run the migrations, and create a .env file like this:

```
ACCESS_KEY_ID=youraccesskeyid
SECRET_ACCESS_KEY=yoursecretaccesskey
REGION=yourregion
BUCKET=yourbucket
```

#### Generating the migration
Active Storage uses two database tables: one to store the filename, content
type etc, and the other to join the attachment to the model that 'owns' it, for
example User.

Running `rails active_storage:install` when you set up a new project generates
the migrations for these tables.

#### Service configuration
Different service types are configured in `config/storage.yml`. Examples of
possible service types are:

- Local Disk
- Amazon S3dw
- Microsoft Azure Storage
- Google Cloud Storage

You then set which service should be used in each environment. For example, in
development, `config.active_storage.service = :local`.

#### Model relations
Attachments are defined as model relations, see the User model in this example.
You can use `has_one_attached` and `has_many_attached` and they do exactly what
you might imagine.

#### Direct uploads
There is support for direct uploads out of the box, just set `direct_upload:
true` on the form field. Uploads begin on form submission.

There are multiple javascript events you can then tap in to (start, initialize,
progress, end etc) to make cool looking uploads.

#### Download links
You can create a download link using the view helper `rails_blob_path`, setting
the disposition. The redirection has an HTTP expiration of 5 mins.

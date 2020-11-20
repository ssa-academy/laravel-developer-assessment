<h1 align="center">
Assessment for Laravel Developer
</h1>

<br>

This assessment is designed to test an examinee’s knowledge of PHP Design principles and its implementations on Laravel framework.

**Assessment Point System**: The assessment total is 60 points with additional 12 bonus points.
Passing grade is 40. See breakdown below for more detail.

|  Points | Bonus | Total |
|  -----: | ----: | ----: |
|      60 |    12 |    72 |

**Asessment Duration**: Examinee is given 2 days to complete the assessment. On a separate spreadsheet, please log the time spent per functionality (start time and end time).
For any questions regarding the exam please send inquiry to <a href="mailto:sandy@ssagroup.com">sandy@ssagroup.com</a> or HR.

**Output**: Examinee is expected to send an email with attachment to their output files (preferably a zip file). Alternatively, examinee can attach a link to their GitHub Repository, Google Drive, Dropbox, or any other storage service to download the output if the file is too large to be attached on email, or for other reason.

<br>
<hr>
<br>

##### Goals

- [ ] Implement Laravel’s default login feature
- [ ] Develop User CRUD functionalities

<br>

##### Prerequisites

Base the user migration file in the following table:

```mysql
mysql> show columns from users;
+-------------------+-----------------+------+-----+---------+----------------+
| Field             | Type            | Null | Key | Default | Extra          |
+-------------------+-----------------+------+-----+---------+----------------+
| id                | bigint unsigned | NO   | PRI | NULL    | auto_increment |
| prefixname        | varchar(255)    | YES  |     | NULL    |                |
| firstname         | varchar(255)    | NO   |     | NULL    |                |
| middlename        | varchar(255)    | YES  |     | NULL    |                |
| lastname          | varchar(255)    | NO   |     | NULL    |                |
| suffixname        | varchar(255)    | YES  |     | NULL    |                |
| username          | varchar(255)    | NO   | UNI | NULL    |                |
| email             | varchar(255)    | NO   | UNI | NULL    |                |
| password          | text            | NO   |     | NULL    |                |
| photo             | text            | YES  |     | NULL    |                |
| type              | varchar(255)    | YES  | MUL | user    |                |
| remember_token    | varchar(100)    | YES  |     | NULL    |                |
| email_verified_at | timestamp       | YES  |     | NULL    |                |
| created_at        | timestamp       | YES  |     | NULL    |                |
| updated_at        | timestamp       | YES  |     | NULL    |                |
| deleted_at        | timestamp       | YES  |     | NULL    |                |
+-------------------+-----------------+------+-----+---------+----------------+
```

<br>

##### Instructions

1. Start a project in Laravel 7 or higher
1. Implement the default login feature using the [laravel/ui](https://packagist.org/packages/laravel/ui) package.
1. Add a page to list all users (users.index) in a table.
1. Add a page to display a single user (users.show).
1. Add a page to display the form to create a new user (users.create).
1. Add a page to edit a user (users.edit / users.update).
1. Add a button to delete a user (users.destroy).
1. Add a page to list all soft deleted users (users.trashed).
1. Add a button to restore a soft deleted user (users.restore).
1. Add a button to permanently delete a soft deleted user (users.delete).

<br>

##### ✎ Notes
- All users routes must implement the `auth` middleware.
- The value for `prefixname` should only be one in `[Mr, Mrs, Ms]`.
- Use `enctype=multipart/form-data` attribute on the `forms` to enable uploading of user photo.

<br>

##### ★ Bonus

- **+5 points** - Write and register a route macro for soft deletes, which can be used as:
	```php
	Route::softDeletes('users', 'UserController');
	```

	which contains the following route collection:
	```php
	Route::get('users/trashed', 'UserController@trashed')->name('users.trashed');
	Route::patch('users/{user}/restore', 'UserController@restore')->name('users.restore');
	Route::delete('users/{user}/delete', 'UserController@delete')->name('users.delete');
	```

- **+2 points** - Implement a model accessor called `getAvatarAttribute` which can be used as:
	```php
	$user = User::find(1);
	$user->avatar;
	```

	<details>
	<summary>which returns the photo or a default image</summary>

	```php
	/**
	 * Retrieve the default photo from storage.
	 * Supply a base64 png image if the `photo` column is null.
	 *
	 * @return string
	 */
	public function getAvatarAttribute(): string
	{
		// Code goes brrrr.
	}
	```
	</details>

- **+2 points** - Implement a model accessor called `getFullnameAttribute` which can be used as:
	```php
	$user = User::find(1);
	$user->fullname; // E.g. Juan P. dela Cruz
	```
	<details>
	<summary>which returns the first, middle initial, and last name of the user</summary>

	```php
	/**
	 * Retrieve the user's full name in the format:
	 *  [firstname][ mi?][ lastname]
	 * Where:
	 *  [ mi?] is the optional middle initial.
	 *
	 * @return string
	 */
	public function getFullnameAttribute(): string
	{
		// Code goes brrrrr.
	}
	```
	</details>

- **+2 points** - Implement a model accessor called `getMiddleinitialAttribute` which can be used as:
	```php
	$user = User::find(1);
	$user->middleinitial; // E.g. "delos Santos" -> "D."
	```

- **+1 point** - Style the pages using a preferred framework (e.g. bootstrap, vuetify, etc.).

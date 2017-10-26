A note on layouts

# default

yes this is default.

# page

Used for all pages (uses default)

# post

unused

# sign_up

stale, unused, should probably be deleted

# medialist

lists all media based on
* talks_files
* other_files

both are lists to be defined in the front matter

# medialist_auto

Lists all talk media residing in `/media/<eventname>/Talks` under the Talks section.
Similar for "Oher" subdirectory.

Any text written in the `content` part of the file using the layout will be added netween the title and the `Talks` section

(it ought to be automatic, but directory handling is weird)

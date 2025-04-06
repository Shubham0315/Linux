What is the difference between soft link and hard link?
-
- Soft link is a pointer or shortcut to another file or directory.
  - It points to file name not actual data
  - If original file is deleted. soft link is broken
  - Command :- **ln -s $file $Link_name**
  -         :- ln -s /home/user/file.txt shortcut.txt
 
- Hard link is another name for the same file data (inode) on the disk
  - Points directly to inode (data) of the file
  - If original file is deleted, data still exists via hard link
  - Command :- ln $file $link_name
  -         :- ln file.txt hardlink.txt
  - Both file.txt and hardlink.txt has same data

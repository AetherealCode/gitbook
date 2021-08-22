# ln \(Unix\)

## ln \(Unix\) 

The **`ln`**command is a standard [Unix command](https://en.m.wikipedia.org/wiki/Unix_command) utility used to create a [hard link](https://en.m.wikipedia.org/wiki/Hard_link) or a [symbolic link](https://en.m.wikipedia.org/wiki/Symbolic_link) \(symlink\) to an existing file. The use of a hard link allows multiple [filenames](https://en.m.wikipedia.org/wiki/Filenames) to be associated with the same [file](https://en.m.wikipedia.org/wiki/Computer_file) since a hard link points to the [inode](https://en.m.wikipedia.org/wiki/Inode) of a given file, the data of which is stored on [disk](https://en.m.wikipedia.org/wiki/Hard_disk_drive). On the other hand, symbolic links are special files that refer to other files by [name](https://en.m.wikipedia.org/wiki/Filename#References:_absolute_vs_relative).  


| [Developer\(s\)](https://en.m.wikipedia.org/wiki/Software_developer)  | [AT&T Bell Laboratories](https://en.m.wikipedia.org/wiki/AT%26T_Bell_Laboratories)  |
| :--- | :--- |
| Initial release  | November 3, 1971; 48 years ago  |
| [Operating system](https://en.m.wikipedia.org/wiki/Operating_system)  | [Unix](https://en.m.wikipedia.org/wiki/Unix) and [Unix-like](https://en.m.wikipedia.org/wiki/Unix-like)  |
| [Type](https://en.m.wikipedia.org/wiki/Software_categories#Categorization_approaches)  | [Command](https://en.m.wikipedia.org/wiki/Command_%28computing%29)  |

The ln command by default creates hard links, and when called with the [command line](https://en.m.wikipedia.org/wiki/Command-line_interface) [parameter](https://en.m.wikipedia.org/wiki/Command-line_interface#Application_command-line_interfaces) ln -s creates symbolic links.[ ](https://en.m.wikipedia.org/wiki/Ln_%28Unix%29?do=export_xhtml&version=41812&translate=1#cite_note-3)Most [operating systems](https://en.m.wikipedia.org/wiki/Operating_systems) prevent hard links to [directories](https://en.m.wikipedia.org/wiki/Directory_%28computing%29) from being created since such a capability could disrupt the structure of a [file system](https://en.m.wikipedia.org/wiki/File_system) and interfere with the operation of other utilities. The ln command can however be used to create symbolic links to non-existent files.  


### History 

The version of ln bundled in [GNU](https://en.m.wikipedia.org/wiki/GNU) [coreutils](https://en.m.wikipedia.org/wiki/Coreutils) was written by Mike Parker and David MacKenzie.  


### Links 

Links allow more than one filename to refer to the same file as in the case of a [hard link](https://en.m.wikipedia.org/wiki/Hard_link) or act as [pointers](https://en.m.wikipedia.org/wiki/Reference_%28computer_science%29) to a filename as in the case of a [soft link](https://en.m.wikipedia.org/wiki/Symbolic_link). Both hard links and soft links can be created by the ln command. Specifically,  


1. [Hard links](https://en.m.wikipedia.org/wiki/Hard_link), also known simply as links, are objects that associate the filename with the [inode](https://en.m.wikipedia.org/wiki/Inode), and therefore the file contents itself. A given file on disk could have multiple links scattered through the [directory hierarchy](https://en.m.wikipedia.org/wiki/Directory_structure), with all of the links being equivalent since they all associate with the same [inode](https://en.m.wikipedia.org/wiki/Inode). Creating a link therefore does not copy the contents of the file but merely causes another name to be associated with the same contents. Each time a hard link is created, a [link counter](https://en.m.wikipedia.org/wiki/Reference_counting#File_systems) that is a part of the [inode structure](https://en.m.wikipedia.org/wiki/Inode#POSIX_inode_description) gets incremented; a file is not deleted until its reference count reaches zero. However, hard links can only be created on the same [file system](https://en.m.wikipedia.org/wiki/File_system); this can prove to be a disadvantage. 
2. [Symbolic links](https://en.m.wikipedia.org/wiki/Symbolic_link) are special files which, when encountered during pathname resolution, modify the [pathname resolution](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_13) to be taken to the location which the symbolic link contains. The content of the symbolic link is therefore the destination [path](https://en.m.wikipedia.org/wiki/Path_%28computing%29) string, which can also be examined using the readlink command line utility. The symbolic link may contain an arbitrary string which does not refer to the location of an existing file. Such a symbolic link will fail until a file is created at the location which is contained by the symbolic link. By contrast, a symbolic link to an existing file will fail if the existing file is moved to a different location \(or renamed\) 

### Specification 

The ln utility on systems compliant with the [Single Unix Specification](https://en.m.wikipedia.org/wiki/Single_Unix_Specification) is specified in the Shell and Utilities \(XCU\) document, which forms a part of the Single Unix Specification  
The specification describes two ways of invoking the ln utility. Specifically, 

In the "single file" invocation the ln utility creates a new hard link \(directory entry\) for the source file specified by the source\_file operand at the destination path specified by the target\_file operand. However, if the -s option is specified, a symbolic link is created.  
`ln [-fs] [-L|-P] source_file target_file`  
In the "multiple file" invocation the ln utility creates a new hard link \([directory entry](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap03.html#tag_03_130)\), or if the -s option is specified, a symbolic link, for each file specified by the source\_file operand, at a destination path in an existing directory named by operand target\_dir.  
`ln [-fs] [-L|-P] source_file_1 source_file_2 ... target_dir`  


The specification also specifies the command line options that must be supported:  
`-f` Force existing destination pathnames to be removed to allow the link.  
`-L` For each source\_file operand that names a file that is a symbolic link, create a hard link to the file referenced by the symbolic link.  
`-P` For each source\_file operand that names a file that is a symbolic link, create a \(hard\) link to the symbolic link itself.  
`-s` Create symbolic links instead of hard links. If the -s option is specified, the -L and -P options are silently ignored.  
If more than one of the mutually-exclusive options -L and -P is specified the last option specified determines the behavior of the utility.  
If the -s option is not specified and neither a -L nor a -P option is specified, the implementation defines which of the -L and -P options will be used as the default.  
If neither target file nor target directory are specified, links will be created in the current [working directory](https://en.m.wikipedia.org/wiki/Working_directory).  



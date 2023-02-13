# Lab 3: Introduction to C++ : Classes, FileIO and the Singleton Design Pattern.
For your lab this week, you will be constructing a singly linked list using a C++ class. This lab will serve as a soft introduction to programming in C++. Your task is to implement a singly linked list. You will represent each node using a C++ class object. Additionally,  you will be performing File I/O for reading in the data for your linked list nodes. Your FileIO class shall follow the singleton design pattern.


# Preliminaries 
Your linked list node should be constructed using the following class.
```c++
class StudentNode{
  public : 
        std::string  name_;
	float         gpa_;
	int totalCredits_;
        StudentNode* next_;
        StudentNode();
        StudentNode(std::string fileName);
	static FileIO file_handler;

};

```


## File I/O in C++
Consult the <a href="https://www.cplusplus.com/reference/fstream/ifstream/">ifstream</a> and  <a href="https://www.cplusplus.com/reference/fstream/ofstream/ofstream/">ofstream</a> reference page for C++ File I/O.
An example: 

```c++
#include <fstream> // header file that provides support for file input and output.

int main(){
	
	std::fstream fs; /* You may also be more specific here, by creating an input or output file stream
			   * i.e.  std::ifstream ifs -- input file stream object std::ofstream ofs -- output file stream object
	fs.open("myfile.bin", ios::in | ios::binary); 
	// This will open a file named `myfile.txt' 
	// `ios::in` -- this sets up the stream for input operations -- 
	// `ios::binary` -- this opens the file in binary mode.
	// CAN YOU OPEN UP A FILE STREAM FOR BOTH READING AND WRITING?
	
	if( fs.is_open() ){ // returns a bool value to validate whether or not the stream object is associated with an open file.
	 // Let's read in some data.
	 int num; // assuming we have some integer value to read in.
	 fs >> num; // We use the stream extraction operator `>>` to extract data from the stream.
	 	     // You may use the stream insertion operator `<<` to insert data into an ofstream object.
	  // The fstream object has a set of flags we can query to check if read-write operations were succesful.
	 
	   /* 1.) badbit - checked with fs.bad(). This returns true if reading or writing operations fail. The failure here is with regards to
	      		   The buffer associated with the stream. In other words, if we try to write to a file that is not open for writing or 
			   if we attemptwriting to a device that has no space left.
	       
	`.    2.) Failbit - checked with fs.fail() - trigerred in the same cases as  fs.bad(). However, it's also set to true when there is a
			    format error. For example, attempting to extract an integer from the stream into an alphabetical character.
			    
	      3.) eofbit     - end of file - checked with fs.eof(). This returns true if a file open for reading has reached the end of the file.
	      
	      4.) goodbit     - checked with fs.good(). Returns false in the same cases where all others return true. 
	      
	      You may also use the NOT (bang) operator `!` which returns true if either failbit or badbit is set to true.
	
	   */
	
	}
	fs.close(); // close the file stream
	

	return 0;
}

```

Your  `FileIO` class should have the following structure. This class will follow a singleton design pattern. Be sure to perform the necessary class setup (as in below) to realize the singleton design implementation.

```c++
class FileIO{
  public : 
        std::string read_line();
	void open_file(const std::string& filename);
	void close_file();
	void write(const std::string& output_filename);

};

```





# Singleton Design Pattern

```cpp

class Singleton{

  public: 
        static Singleton& getInstance();
        Singleton(Singleton const& ) = delete; // copy constructor;
        Singleton& operator=(Singleton const&) = delete; // copy assignment
        Singleton(Singleton &&) = delete; // move constructor
        Singleton& operator = (Singleton &&) = delete; // move assignment
        ~Singleton();
	void foo() { std::cout << __PRETTY_FUNCTION__ << std::endl;}
  private:
      Singleton(){}
}

int main(int argc, char* argv[]){

	// To get an instance of our singleton, we define a C++ reference variable and bind it to the
	// reference returned by the getInstance() method. That is, we give the singleton instance a name.
	Singleton &singleton_instance = Singleton::getInstance();
	singleton_instance.foo();
	
	return 0;
}
```

# Instructions 
- Make commits as often as necessary, with self-contained bits of code rather than large blobs. ***You do not need to push after each commit.***
- Itemized directions are below. You may not have to do them in order.

1. Read and internalize the warnings.
2. Create a `main.cpp` OR `main.cc` file. **N.B**: The C++ compiler recognizes either extension for Cplusplus source code files.
	- Include the `argc` and `argv` arguments for the main function. For this assignment, you will be reading the node data from a text file.
	- Use the command line arguments to pass in the file name **more on this later..**.  
3. Create a header and implementation file for a studentList. 
	- Define a C++ class for a student Node following the above example.
	- Your class should include a default constructor which just creates an instance of the class with all data members set to null.
	- Since the data for the Linked List will be read in from a file, you should also implement a constructor which takes in a file name as a parameter. 
		- This constructor should go through every student in the file and create and link a node for each respective student.
	- Each student file will follow this format:
		``` 
		Name
		GPA
		Total credits
		```
	- Implement a function to print list to standard out using the following format:
			- ```Student Name: #####\nGPA: #####\nTotal credits: ####```
				- Replace the hashes with the actual data. 
	- Implement a function to print the contents of the list to a file with the following format:
		``` 		
		Name
		GPA
		Total credits
		\n
		Name
		GPA
		Total credits
		...
		```	
		
4. Dynamically allocate students and nodes with C++'s `new` keyword.
6. Test all of your functions in `main`.
7. Add **ROBUST** error handling to deal with the command line input!!
9. Print meaningful error messages to standard out. Such as ```c++ std::cout << "Could not delete student `" << student << "` . The student does not exist!"<< std::endl; ```
	
# Getting Started
Get your personal link and invoke `git clone {linkhere}`, which should be a combination of your username and the name of the lab.

# Compiling
The repository does not include a makefile, so you'll need to create your own. The instructors should be able to compile the code by invoking `make`. Additionally, `make clean` should remove all files that are not source code.


# Running
The instructors should be able to run the code by invoking the executable, `./linkedList`, or by running `make run`.

# <span style="color:red">Warning</span>
<span style="color:red">Failure to heed the following statements may result in lost points.</span>
- Valgrind will be used on your assignments and be a critera for grading.
- Do not push unneeded files, such as those created during compilation.
- It is advised to do the lab assignment first, and then any extra credit you want to attempt. Your submission's grade is much more dependent on the core instructions. 
- Do not use `malloc` in this assignment. Use C++'s `new` and `delete` keyword for heap memory management instead.
- Test all of your functions in `main`.
- Use some sort of error handling, such as if-else statements that use `std::cout` to write warnings to the console.
- Be sure to perform substantial error checking on the command line options.

Example valgrind output that would not result in a loss of points:
```
==18852== 
==18852== HEAP SUMMARY:
==18852==     in use at exit: 0 bytes in 0 blocks
==18852==   total heap usage: 24 allocs, 24 frees, 3,952 bytes allocated
==18852== 
==18852== All heap blocks were freed -- no leaks are possible
==18852== 
==18852== For counts of detected and suppressed errors, rerun with: -v
==18852== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```

## Gitignore
All submissions must not include any extraneous files, which includes intermediate files used in compilation. One simple but tedious way to achieve this is to not stage and commit unnwanted files. However, a more efficient way exists that won't take up space in a `git status` command.

You may use a `.gitignore` file, which supports the wildcard `*`. A good reference is provided here: https://linuxize.com/post/gitignore-ignoring-files-in-git/ 
First, you need to create the file with `touch .gitignore` or `vim .gitignore`. Nano can probably be used as well, but it is not explicitly mentioned here because it is inferior to vim. Make sure to include the `.` character.

The `.gitignore` file should contain one pattern per line. Directories may be included as well. A small example is below and will need to be augmented to ignore all of the unwanted files.
```
*.o
build/
```

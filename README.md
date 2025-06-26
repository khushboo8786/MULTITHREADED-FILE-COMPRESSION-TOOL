# MULTITHREADED-FILE-COMPRESSION-TOOL

*COMPANY*:CODTECH IT SOLUTIONS

*NAME*:KHUSHBOO KUMARI

*INTERN ID*:CT04DN1859

*DOMAIN*:C++

*MENTOR*:NEELA SANTHOSH KUMAR

**This C++ program implements a simple and efficient multithreaded file compression and decompression tool based on the Run-Length Encoding (RLE) algorithm. The primary objective of the code is to handle large files by breaking them into manageable chunks, compress or decompress them concurrently using multiple threads, and finally write the processed data to an output file. The design leverages modern C++ features such as the Standard Template Library (STL), threading (<thread>), and synchronization mechanisms (<mutex>), ensuring both scalability and performance.

Core Components and Functionality
1. Constants and Global Variables
CHUNK_SIZE: Defined as 1 MB (1024 * 1024 bytes), this constant determines the size of data read and processed in each chunk. It allows the program to handle large files in smaller segments to efficiently utilize system memory.

io_mutex: A global mutex used to synchronize console output across multiple threads, preventing interleaved or garbled logging.

2. Run-Length Encoding (RLE) Implementation
compress_rle(const std::string& data):
This function performs RLE compression on a given input string. It iterates through the string, counts consecutive occurrences of each character (up to 255), and appends the character followed by its count as a single unit in the compressed string. For example, the input "aaaabb" would become "a\x04b\x02".

decompress_rle(const std::string& data):
This function performs the reverse operation of compress_rle. It reads each character and the following byte (representing the count) and reconstructs the original string by repeating the character according to the count.

3. Threaded Chunk Processing
compress_chunk and decompress_chunk:
These are thread functions responsible for processing individual data chunks. Each function takes the input chunk, applies the respective RLE algorithm, stores the result in a shared results vector, and logs the completion status using a thread-safe lock (std::lock_guard with io_mutex).

4. File Processing Workflow
process_file(const std::string& filename, bool compressing):
This function is the heart of the program’s file I/O and multithreading logic. Its workflow includes:

Opening Input File: The input file is opened in binary mode for reading.

Chunking: Data is read in blocks of 1 MB and stored in a chunks vector. The actual bytes read are resized to fit the buffer to avoid trailing null bytes.

Launching Threads: For each chunk, a thread is created to either compress or decompress the data, depending on the compressing flag.

Joining Threads: All threads are joined to ensure completion before moving to the next stage.

Writing Output File: The processed chunks are written sequentially into either "compressed.rle" or "decompressed.txt", depending on the operation mode.

5. Entry Point: main() Function
The main() function serves as the command-line interface. It expects two arguments:

Operation mode: "compress" or "decompress"

Input file name

Based on the operation mode, it invokes process_file with the appropriate flag. If incorrect arguments are supplied, it prints a usage message.

Thread Safety and Performance Considerations
Thread safety is crucial in multithreaded programs, especially when accessing shared resources like the console (std::cout). This program ensures synchronized output using a mutex (io_mutex). However, note that the chunks and results vectors are accessed in a thread-safe manner by pre-allocating space before threads are spawned and using unique references (std::ref) to prevent data races.

Moreover, since each thread works on a separate segment of data and the algorithm is inherently parallelizable, the program demonstrates good scalability on multi-core systems, significantly improving performance compared to single-threaded approaches.

Use Cases and Limitations
This tool is ideal for compressing large text or binary files that contain many repeating characters. However, RLE is not optimal for data with high entropy (e.g., already compressed files or random data), as it may not reduce file size effectively.

Error handling is minimal in this implementation. For instance, there are no checks for file read/write failures beyond opening the input file. Additionally, the RLE format used here is simplistic and does not include headers or metadata, making it unsuitable for use in systems requiring robust file format specifications.

Conclusion
In summary, this C++ program demonstrates the use of multithreading, efficient file I/O, and a basic compression algorithm to implement a simple yet effective file compression/decompression utility. The modular design and clear separation of concerns make the code maintainable and extensible, while the use of modern C++ features reflects practical software engineering principles. It is a strong foundation for further improvements such as more sophisticated compression schemes, error handling, and performance optimizations.

*OUTPUT*:![Image](https://github.com/user-attachments/assets/24b60c3e-3e0b-49c2-b575-e27ff673659f)



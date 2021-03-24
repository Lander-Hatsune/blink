cmake_minimum_required(VERSION 3.10)

project(file-transfer VERSION 0.1)

# file-send
add_executable(file-send ./send.c)
target_link_libraries(file-send -I ./libquiche.a)

# file-recv
add_executable(file-recv ./recv.c)
target_link_libraries(file-recv -I ./libquiche.a)


include_directories ("${PROJECT_SOURCE_DIR}/src")

add_executable(io_tests io_tests.c tests.c)
add_test(io_tests io_tests)
target_link_libraries(io_tests books cmocka)

add_executable(book_tests book_tests.c tests.c)
add_test(book_tests book_tests)
target_link_libraries(book_tests books cmocka)

add_test(io_test_valgrind valgrind
         --error-exitcode=1 --read-var-info=yes
         --leak-check=full --show-leak-kinds=all -v
         ./io_tests)

add_test(book_tests_valgrind valgrind
         --error-exitcode=1 --read-var-info=yes
         --leak-check=full --show-leak-kinds=all -v
         ./book_tests)

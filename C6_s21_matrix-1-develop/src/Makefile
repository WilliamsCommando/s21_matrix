.PHONY: all clean test s21_matrix.a gcov_report
OS := $(shell uname -s)
CC = gcc
FLAG = -Wall -Werror -Wextra
FLAG_C = -c -Wall -Werror -Wextra
CL_11 = -std=c11
ALL_FILE = s21_matrix.c
ALL_FILE_O = s21_matrix.o

ifeq ($(OS), Darwin)
	FLAGS_PLATFORM = -lcheck
else
	FLAGS_PLATFORM = -lcheck -lrt -lm -lpthread
endif

all: clean s21_matrix.a

s21_matrix.a:
	@$(CC) $(FLAG_C) $(ALL_FILE)
	@ar rcs s21_matrix.a $(ALL_FILE_O)

test: s21_matrix.a
	@gcc s21_test_matrix.c s21_matrix.a $(FLAGS_PLATFORM) -g -o tests.o
	@./tests.o

gcov_report:
	@$(CC) --coverage $(ALL_FILE) s21_test_matrix.c $(FLAGS_PLATFORM) -o gcov_report.o
	@./gcov_report.o
	@lcov -t s21_matrix_tests -o s21_matrix_tests.info -c -d .
	@genhtml -o gcov_report s21_matrix_tests.info
	@open ./gcov_report/index.html

clean:
	@rm -f *.a
	@rm -f s21_matrix
	@rm -f *.o
	@rm -f *.txt
	@rm -f *.gcda
	@rm -f *.gcdo
	@rm -f *.gcno
	@rm -f *.info
	@rm -rf *.dSYM
	@rm -rf ./gcov_report

clint:
	@clang-format -i *.c *.h
	@clang-format -n *.c *.h
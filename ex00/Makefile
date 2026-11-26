NAME = convert

CXX = c++ -g

SRCS = main.cpp ScalarConverter.cpp

OBJS = $(addprefix ./, $(SRCS:.cpp=.o))

CXXFLAGS = -Wall -Wextra -Werror -std=c++98 -pedantic

all: $(NAME)

$(NAME): $(OBJS)
	$(CXX) $(CXXFLAGS) $(OBJS) -o $@

%.o: %.cpp
	$(CXX) $(CXXFLAGS) -c $< -o $@

cppformat:
	clang-format -i $(SRCS) *.hpp

cpplint:
	clang-tidy --config-file=.clang-tidy --warnings-as-errors=* --quiet $(SRCS) *.hpp -- -Wall -Wextra -Werror -std=c++98

clean:
	rm -f $(OBJS)

fclean: clean
	rm -f $(NAME)

re: fclean all

test: $(NAME)
	./convert 0
	@printf '%s\n' \
		'outputs should be:' \
		'char: Non displayable' \
		'int: 0' \
		'float: 0.0f' \
		'double: 0.0'
	./convert nan
	@printf '%s\n' \
		'outputs should be:' \
		'char: impossible' \
		'int: impossible' \
		'float: nanf' \
		'double: nan'
	./convert 42.0f
	@printf '%s\n' \
		'outputs should be:' \
		"char: '*'" \
		'int: 42' \
		'float: 42.0f' \
		'double: 42.0'

.PHONY: all clean fclean re cppformat cpplint test

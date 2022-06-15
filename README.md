TECHNICAL ASSESSMENT FOR FULL STACK DEVELOPER (Vue.JS & DJANGO)

1. Explain Q objects in Django ORM? With example

SOLUTION:

A Q() object represents an SQL condition that can be used in database-related operations. It’s similar to how an F() object represents the value of a model field or annotation. They make it possible to define and reuse conditions, and combine them using operators such as | (OR) and & (AND).

For instance, given the following model:

class Entry(models.Model):
    		headline = models.CharField(max_length=255)
    		body_text = models.TextField()
    		pub_date = models.DateField()
    		mod_date = models.DateField(default=date.today)
    		number_of_comments = models.IntegerField(default=0)
    		number_of_pingbacks = models.IntegerField(default=0)
    		rating = models.IntegerField(default=5)


my_or_query = Q(headline__startswith='Who') | Q(headline__startswith='What')

The above query returns a queryset comprising of entries that have a headline that starts with ‘Who’ OR ‘What’.

my_and_query = Q(headline__startswith='Who') & Q(headline__pubdate__gte=datetime.date(2025, 5, 30)
)

The above query returns a queryset comprising of entries that have a headline that starts with ‘Who’ AND have a pub_date greater than or equal ‘30-5-2025’.



2. What are Directives in VUE.js, List some of them you used?

SOLUTION:

Essentially, a directive is some special token in the markup that tells the library to do something to a DOM element.

Some examples I have used include:

    • v-text
    • v-show
    • v-if
    • v-else
    • v-else-if
    • v-for
    • v-on
    • v-bind

3. There are n houses built in a line. A thief wants to steal the maximum possible money from these houses. The only restriction the thief has is that he can’t steal from two consecutive houses, as that would alert the security system. How should the thief maximize his stealing?
Problem Statement
Given a number array representing the wealth of n houses, determine the maximum amount of money the thief can steal without alerting the security system.
Example 1:
Input: {2, 5, 1, 3, 6, 2, 4} Output: 15 Explanation: The thief should steal from houses 5 + 6 + 4
Example 2:
Input: {2, 10, 14, 8, 1} Output: 18 Explanation: The thief should steal from houses 10 + 8

SOLUTION:

def maximize_loot(houses, num_houses):
	if num_houses == 0:
		return 0

	loot1 = houses[0]
	if num_houses == 1:
		return loot1

	loot2 = max(houses[0], houses[1])
	if num_houses == 2:
		return loot2

	# contains maximum stolen value at the end
	max_loot = None

	# Fill remaining positions
	for i in range(2, num_houses):
		max_loot = max(houses[i]+loot1, loot2)
		loot1 = loot2
		loot2 = max_loot

	return max_loot

# test above code
def main():
	# Value of houses
	houses = [2, 5, 1, 3, 6, 2, 4]

	# number of houses
	num_houses = len(houses)
	print(f"Maximum loot value : {maximize_loot(houses, num_houses)}")

if __name__ == '__main__':
	main()

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int next_permutation(int n, char **s)
{
  
    for (int i = n - 1; i > 0; i--)
        if (strcmp(s[i], s[i - 1]) > 0)
        {
            int j = i + 1;
            for (; j < n; j++)
            if (strcmp(s[j], s[i - 1]) <= 0)
            break;
            char *t = s[i - 1];
            s[i - 1] = s[j - 1];
            s[j - 1] = t;
            for (; i < n - 1; i++, n--)
            {
                t = s[i];
                s[i] = s[n - 1];
                s[n - 1] = t;
            }
            return 1;
        }
    for (int i = 0; i < n - 1; i++, n--)
    {
        char *t = s[i];
        s[i] = s[n - 1];
        s[n - 1] = t;
    }
    return 0;
}

int main()
{
	char **s;
	int n;
	scanf("%d", &n);
	s = calloc(n, sizeof(char*));
	for (int i = 0; i < n; i++)
	{
		s[i] = calloc(11, sizeof(char));
		scanf("%s", s[i]);
	}
	do
	{
		for (int i = 0; i < n; i++)
			printf("%s%c", s[i], i == n - 1 ? '\n' : ' ');
	} while (next_permutation(n, s));
	for (int i = 0; i < n; i++)
		free(s[i]);
	free(s);
	return 0;
}

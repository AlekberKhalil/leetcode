# Employee Importance

You are given a data structure of employee information, which includes the employee's**unique id**, his**importance value**and his**direct**subordinates' id.

For example, employee 1 is the leader of employee 2, and employee 2 is the leader of employee 3. They have importance value 15, 10 and 5, respectively. Then employee 1 has a data structure like \[1, 15, \[2\]\], and employee 2 has \[2, 10, \[3\]\], and employee 3 has \[3, 5, \[\]\]. Note that although employee 3 is also a subordinate of employee 1, the relationship is**not direct**.

Now given the employee information of a company, and an employee id, you need to return the total importance value of this employee and all his subordinates.

**Example 1:**

```text
Input: [[1, 5, [2, 3]], [2, 3, []], [3, 3, []]], 1Output: 11Explanation:Employee 1 has importance value 5, and he has two direct subordinates: employee 2 and employee 3. They both have importance value 3. So the total importance value of employee 1 is 5 + 3 + 3 = 11.
```

**Note:**

```text
One employee has at most one direct leader and may have several subordinates.The maximum number of employees won't exceed 2000.
```

分析

员工建map。dfs子员工下去

```text
"""# Employee infoclass Employee:    def __init__(self, id, importance, subordinates):        # It's the unique id of each node.        # unique id of this employee        self.id = id        # the importance value of this employee        self.importance = importance        # the id of direct subordinates        self.subordinates = subordinates"""class Solution:    def getImportance(self, employees, id):        """        :type employees: Employee        :type id: int        :rtype: int        """        def dfs(e):            a,b,c = e.id,e.importance,e.subordinates            if len(c) == 0:                return b            return b + sum([dfs(mm[i]) for i in c])        mm = collections.defaultdict()            for e in employees:            mm[e.id] = e        return dfs(mm[id])
```


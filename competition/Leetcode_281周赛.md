# 6012. 统计各位数字之和为偶数的整数个数
## 题目
给你一个正整数 num ，请你统计并返回 小于或等于 num 且各位数字之和为 偶数 的正整数的数目。

正整数的 各位数字之和 是其所有位上的对应数字相加的结果。

 

示例 1：
```
输入：num = 4
输出：2
解释：
只有 2 和 4 满足小于等于 4 且各位数字之和为偶数。 
```   
示例 2：
```
输入：num = 30
输出：14
解释：
只有 14 个整数满足小于等于 30 且各位数字之和为偶数，分别是： 
2、4、6、8、11、13、15、17、19、20、22、24、26 和 28 。
```
## 代码
```c++
class Solution {
public:
    int countEven(int num) {
        int res = 0;
        for(int i = 1;i <= num;i ++)
        {
            if(check(i)) res ++;
        }
        return res;
    }
    bool check(int num){
        int sum = 0;
        while(num) {
            sum += num % 10;
            num = num / 10;
        }
        return sum % 2 == 0;
    }
};
```
# 6013. 合并零之间的节点
## 题目
给你一个链表的头节点 head ，该链表包含由 0 分隔开的一连串整数。链表的 开端 和 末尾 的节点都满足 Node.val == 0 。

对于每两个相邻的 0 ，请你将它们之间的所有节点合并成一个节点，其值是所有已合并节点的值之和。然后将所有 0 移除，修改后的链表不应该含有任何 0 。

 返回修改后链表的头节点 head 。

 

示例 1：

```
输入：head = [0,3,1,0,4,5,2,0]
输出：[4,11]
解释：
上图表示输入的链表。修改后的链表包含：
- 标记为绿色的节点之和：3 + 1 = 4
- 标记为红色的节点之和：4 + 5 + 2 = 11
```
示例 2：

```
输入：head = [0,1,0,3,0,2,2,0]
输出：[1,3,4]
解释：
上图表示输入的链表。修改后的链表包含：
- 标记为绿色的节点之和：1 = 1
- 标记为红色的节点之和：3 = 3
- 标记为黄色的节点之和：2 + 2 = 4
```
## 代码
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeNodes(ListNode* head) {
        ListNode* dummy  = new ListNode(-1);
        dummy->next = head;
        auto tail = dummy;
        auto p = head;
        while(p)
        {
            if(p->val == 0) 
            {
                auto q = p->next;
                int sum = 0;
                while(q && q->val != 0)
                {
                    sum += q->val;
                    q = q->next;
                }
                p = q;
                if(sum) tail = tail->next = new ListNode(sum);
            }
        }
        return dummy->next;
    }
};
```
# 
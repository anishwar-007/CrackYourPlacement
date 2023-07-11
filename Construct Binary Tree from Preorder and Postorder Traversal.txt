/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* constructFromPrePost(vector<int>& preorder, vector<int>& postorder) {
        int n = preorder.size() - 1;
        return build(preorder, postorder, 0, n, 0, n);
    }
    TreeNode* build(vector<int>& preorder, vector<int>& postorder,
                    int preLeft, int preRight, int postLeft, int postRight)
    {
        if (preLeft > preRight || postLeft > postRight) return NULL;
        TreeNode* ans = new TreeNode(preorder[preLeft]);
        if (preLeft == preRight) return ans; 
        int len = 1;
        for (;len < preRight - preLeft; len++)
        {
            if (preorder[preLeft + 1] == postorder[postLeft + len - 1])
                break;
        }
        ans->left = build(preorder, postorder, preLeft + 1, preLeft + len, postLeft, postLeft + len - 1);
        ans->right = build(preorder, postorder, preLeft + len + 1, preRight, postLeft + len, postRight - 1);
        return ans;
    }
};
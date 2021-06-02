并查集
********



instance::

    func findCircleNum(isConnected [][]int) (ans int) {
    n := len(isConnected)
    parent := make([]int, n)
    for i := range parent {
        parent[i] = i
    }
    var find func(int) int
    find = func(x int) int {
        if parent[x] != x {
            parent[x] = find(parent[x])
        }
        return parent[x]
    }
    union := func(from, to int) {
        parent[find(from)] = find(to)
    }

    for i, row := range isConnected {
        for j := i + 1; j < n; j++ {
            if row[j] == 1 {
                union(i, j)
            }
        }
    }
    for i, p := range parent {
        if i == p {
            ans++
        }
    }
    return
    }

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/number-of-provinces/solution/sheng-fen-shu-liang-by-leetcode-solution-eyk0/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
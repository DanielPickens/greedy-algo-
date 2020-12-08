int jump(int[] nums, int n) {
    int previous = 0
    int current = 0 
    int jumps = 0
    for(int i = 0 to i < n) {
        if(i > previous) {
            jumps = jumps + 1
            previous = current
        }
        current = max(current, i + nums[i])
    }
    return jumps

1.手写call

    Function.prototype.call = function(context) {
        var ctx = context || window;
        // 将当前调用的方法定义在ctx上，为了能以对象的调用的形式绑定this
        ctx.func = this;
        // 获取参数
        var args = Array.from(arguments).slice(1);
        // 获取函数执行结果
        var res = args.length > 0 ? ctx.func(...args) : ctx.func();
        // 删除func属性
        delete ctx.func;
        // 返回结果
        return res;
    }


2.手写bind

    Function.prototype.bind = function(context) {
        var ctx = context || window;
        // 将当前调用的方法定义在ctx上，为了能以对象的调用的形式绑定this
        ctx.func = this;
        // 获取参数
        var args = Array.from(arguments).slice(1);

        return function() {
            var allArgs = args.concat(Array.from(arguments));

            return allArgs.length > 0 ? ctx.func(...allArgs) : ctx.func()
        }
    }

3.手写深拷贝


    function deepClone(target) {
        var result;

        if(typeof target === 'object') {
            if(Array.isArray(target)) {
                result = [];
                for(let i in target) {
                    result[i] = deepClone(target[i]);
                }
            } else if(target == null) {
                result = null
            } else if(target.constructor === RegExp) {
                result = target;
            } else {
                result = {};
                for(let i in target) {
                    result[i] = deepClone(target[i]);
                }
            }
        } else {
            result = target;
        }

        return result;
    }

4.['1', '2', '3'].map(parseInt)  会输出啥，为啥？




5.接雨水

    给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。 

    示例 1： 
    
        输入：height = [0,1,0,2,1,0,1,3,2,1,2,1] 
        
        输出：6 
        
        解释：上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单 位的雨水（蓝色部分表示雨水）。 
    
    示例 2： 
    
        输入：height = [4,2,0,3,2,5] 
        
        输出：9

    var trap = function(nums) {

        let ans = 0;

        let n = nums.length;

        for(let i = 1; i < n - 1; i++) {
            let l_max = 0, r_max = 0;

            for(let j = 0; j <= i; j++) {
                if(nums[j] > l_max) {
                    l_max = nums[j]
                }
            }

            for(let j = i; j < n; j++) {
                if(nums[j] > r_max) {
                    r_max = nums[j]
                }
            }

            ans += Math.min(l_max, r_max) - nums[i];
        }

        return ans;
    }


    

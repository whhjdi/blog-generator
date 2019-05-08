---
title: LeetCode学习
date: 2019-05-04 20:50:04
tags: [LeetCode]
cover_img:
feature_img:
description:
keywords:
---

## EASY

1. 有效的括号

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

示例 1:

输入: "()"
输出: true
示例 2:

输入: "()[]{}"
输出: true
示例 3:

输入: "(]"
输出: false
示例 4:

输入: "([)]"
输出: false
示例 5:

输入: "{[]}"
输出: true

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
	let valid = true;
	const stack = [];
	const mapper = {
		"{": "}",
		"[": "]",
		"(": ")"
	};

	for (let key in s) {
		let val = s[key];
		if (["{", "[", "("].indexOf(val) > -1) {
			stack.push(val);
			l;
		} else {
			let p = stack.pop();
			if (val !== mapper[p]) {
				valid = false;
			}
		}
	}
	if (stack.length > 0) return false;
	return valid;
};
```

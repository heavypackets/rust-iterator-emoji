Iterator Methods
===

Basic
---

[cloned](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.cloned)
```rust
[🐮, 🥔, 🐔, 🌽]
    .iter()
    .cloned()
    .collect::<Vec<_>>() // [🐮, 🥔, 🐔, 🌽]
```

[collect](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.collect)
```rust
[🐮, 🥔, 🐔, 🌽]
    .iter()
    .collect::<Vec<_>>() // [&🐮, &🥔, &🐔, &🌽]
```

[count](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.count)
```rust
[🐱, 🐶, 🐦].iter().count() // 3 (usize)
```

[last](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.last)
```rust
[🐱, 🐶, 🐦].iter().last() // &🐦 
```

[nth](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.nth)
```rust
[🐱, 🐶, 🐦].iter().nth(1) // &🐶
```

Behavior
---

[cycle](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.cycle)
```rust
list = [🐮, 🥔, 🐔, 🌽]
    .iter()
    .cycle()
    .take(6)
    .collect::<Vec<_>>() // [&🐮, &🥔, &🐔, &🌽, &🐮, &🥔]
```

[rev](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.rev)
```rust
[🐮, 🥔, 🐔, 🌽]
    .iter()
    .rev()
    .collect::<Vec<_>>() // [&🌽, &🐔, &🥔, &🐮]
```

[skip](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.skip)
```rust
[🐮, 🥔, 🐔, 🌽]
    .iter()
    .skip(2)
    .collect::<Vec<_>>() // [&🐔, &🌽]
```

[step_by](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.step_by)
```rust
[🐮, 🥔, 🐔, 🌽]
    .iter()
    .step_by(2)
    .collect::<Vec<_>>() // [&🐮, &🐔]
```

[take](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.take)
```rust
list = [🐮, 🥔, 🐔, 🌽]
    .iter()
    .take(3)
    .collect::<Vec<_>>() // [&🐮, &🥔, &🐔]
```

Combine
---

[chain](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.chain)
```rust
let animals = [🐱, 🐶, 🐦];
let food = [🍰, 🍔, 🍬];
animals.iter()
    .chain(food.iter())
    .collect::<Vec<_>>() // [&🐱, &🐶, &🐦, &🍰, &🍔, &🍬]
```

[flatten](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.flatten)
```rust
vec![vec![🐱, 🐶, 🐦], vec![🍰, 🍔, 🍬]]
    .iter()
    .flatten()
    .collect::<Vec<_>>() // [&🐱, &🐶, &🐦, &🍰, &🍔, &🍬]
```

[unzip](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.unzip)
```rust
let (animals, foods): (Vec<Animal>, Vec<Food>) = 
[(🐱, 🍰), (🐶, 🍔), (🐦, 🍬)]
    .iter()
    .unzip(food.iter());

println!("{:?}", left); // [🐱, 🐶, 🐦]
println!("{:?}", right); // [🍰, 🍔, 🍬]
```

[zip](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.zip)
```rust
let animals = [🐱, 🐶, 🐦];
let food = [🍰, 🍔, 🍬];
animals.iter()
    .zip(food.iter())
    .collect::<Vec<_>>() // [(&🐱, &🍰), (&🐶, &🍔), (&🐦, &🍬)]
```

Recursive
---

[emumerate](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.enumerate)
```rust
[🐱, 🐶, 🐦]
    .iter()
    .enumerate()
    .collect::<Vec<_>>() // [(0, &🐱), (1, &🐶), (2, &🐦)]
```
```rust
for (index, animal) in [🐱, 🐶, 🐦].iter().enumerate() 
{
    println!("{}, {}", index, animal) // "0, 🐱 ", "1, 🐶 ", "2, 🐦 "
}
```

[flat_map](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.flat_map)
```rust
let salad = vec![🥗]
let entree = vec![🍔, 🍟];
let dessert = vec![🍨, 🍰];
let dinner = vec![salad, entree, dessert];

let vegetarian_choices: Vec<Food> = dinner
    .iter()
    .flat_map(|course| {
        course.iter().filter(|&food| is_vegetarian(food))
    })
    .collect(); // [🥗, 🍟, 🍰, 🍨] \TODO aren't these references?
```

[fold](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.fold)
```rust
[🍔, 🍟, 🍨] // calories: 500, 200, 600
    .iter()
    .fold(0, |total_calories, &food| {
        total_calories + food
    }) // 1300
```

[for_each](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.for_each)
```rust
[🐱, 🐶, 🐦]
    .iter()
    .for_each(|&animal| {
        speak(animal) // "meow", "bark", "chirp"
    });
```


[map](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.map)
```rust
[🐮, 🥔, 🐔, 🌽]
    .iter()
    .map(|&ingredient| cook(ingredient))
    .collect::<Vec<_>>() // [🍔, 🍟, 🍗, 🍿]
```

[scan](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.scan)
```rust
[🍔, 🍟, 🍨] // calories: 500, 200, 600
    .iter()
    .scan(0, |total_calories, &food| {
        *total_calories = *total_calories + food;

        Some(total_calories)
    })
    .collect::<Vec<_>>() // [500, 700, 1300]
```

Search & Filter
---

[filter](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.filter)
```rust
[🍔, 🍟, 🍗, 🍿]
    .iter()
    .filter(|&food| is_vegetarian(food))
    .collect::<Vec<_>>() // [&🍟, &🍿]
```

[filter_map](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.filter_map)
```rust
[🐮, 🥔, 🐔, 🌽]
    .iter()
    .filter_map(|&ingredient| {
        if is_vegetable(ingredient) {
            Some(cook(ingredient))
        } else {
            None
        }
    })
    .collect::<Vec<_>>() // [🍟, 🍿]
```

[skip_while](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.skip_while)
```rust
[🐱, 🐶, 🐦, 🍰, 🍔, 🍬, 🐔]
    .iter()
    .skip_while(|&x| is_animal(x))
    .collect::<Vec<_>>() // [&🍰, &🍔, &🍬, &🐔]
```

[take_while](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.take_while)
```rust
[🐱, 🐶, 🐦, 🍰, 🍔, 🍬, 🐔]
    .iter()
    .take_while(|&x| is_animal(x))
    .collect::<Vec<_>>() // [&🐱, &🐶, &🐦]
```

[partition](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.partition)
```rust
let (vegetarian, omnivore): <(Vec<Food>, Vec<Food>)> = [🍔, 🍟, 🍗, 🍿]
    .iter()
    .partition(|food| is_vegetarian(food));
    
println!("{:?}", vegetarian); // [&🍟, &🍿]
println!("{:?}", omnivore); // [&🍔, &🍗]
```

[all](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.all)
```rust
[🍔, 🍟, 🍗, 🍿]
    .iter()
    .all(|&food| is_vegetarian(food)) // false
```
```rust
[🥗, 🍇, 🍅, 🍎]
    .iter()
    .all(|&food| is_vegetarian(food)) // true
```

[any](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.any)
```rust
[🍔, 🍟, 🍗, 🍿]
    .iter()
    .any(|&food| is_vegetarian(food)) // true
```
```rust
[🍔, 🍗, 🍣, 🥓]
    .iter()
    .any(|&food| is_vegetarian(food)) // false
```

[find](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.find)
```rust
[🍔, 🍟, 🍗, 🍿]
    .iter()
    .find(|&food| is_vegetarian(food)) // Some(&🍟)
```
```rust
[🍔, 🍗, 🍣, 🥓]
    .iter()
    .find(|&food| is_vegetarian(food)) // None
```

[find_map](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.find_map)
```rust
[🐮, 🥔, 🐔, 🌽]
    .iter()
    .find_map(|ingredient| {
        if is_vegetable(ingredient) {
            Some(ingredient)
        } else {
            None
        }
    }) // &🥔 
```

[position](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.position)
```rust
[🍔, 🍟, 🍗, 🍿]
    .iter()
    .position(|&food| is_vegetarian(food)) // Some(1)
```
```rust
[🍔, 🍗, 🍣, 🥓]
    .iter()
    .position(|&food| is_vegetarian(food)) // None
```
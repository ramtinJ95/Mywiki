## The only unbreakable law in software engineering

There are a bunch of things in software that we call laws but most of them are
just rules of thumbs and are not really saying anyhting about any emerging
feature in software architecture.

To date, there are really three laws that seem to be true and actually touch
upon something true:
- Amdahls law, which is T(n) = b + (T(1) - b) / n. T(n) is the time it takes for
  some n number of workers to complete a task, b is the part of the program that
  cannot be parallelised. What this laws tells us is that just adding a bunch of
  new workers in a computer or in real life has an asymptotic limit which is
  determined by the part of the task that cannot be done in parallel.

- Brooks law. This is from the mythical man month book where many observation
  where made that just adding  new workers to a project does not neccassarily
  mean that the productivity will go up, in fact if these workers need to
  communicate a lot then the efficiency of the entire team can actually become
  lower, or it will reach its asymptotic limit very rapidly.
  
- Conways law. This law says that the product that a organization will build and
  output will in the best case possible just be a reflection of that
  organizations org chart. This is a super powerful idea because it means that
  they way we split teams in subteams and so on is super important because as
  soon as we decide that some part x and some other part y does not need to be
  in the same team, we are essentially saying that whatever inventions that
  could have come from these 2 components being in close communications is not
  the best one for our situation. But we are doing this without really knowing
  that we are doing it and thus throwing away a huge chunk of the possible
  outcome space that we now will never see. The reason for this is that
  communication between teams is much harder then communication in a team.

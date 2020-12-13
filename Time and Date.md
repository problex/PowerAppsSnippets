# Convert Time Int to TimeValue

Example convert 600 to a TimeValue 06:00 AM

TimeValue(
    Left(
        If(
            Len(Text(600)) = 3,
            0 & Text(600),
            Text(600)
        ),
        2
    ) & ":" & Right(
        If(
            Len(Text(600)) = 3,
            0 & Text(600),
            Text(600)
        ),
        2
    ),
    "EN"
)



# Check for Time Conflicts

ForAll(
    TimeCheck,
    If(
        StartTime > StartTimeAssignee && StartTime < EndTimeAssignee || EndTime < EndTimeAssignee && EndTime > StartTimeAssignee || StartTime < EndTimeAssignee && EndTime > StartTimeAssignee,
        Collect(
            TimeCheckResult,
            Id
        )
    )
);
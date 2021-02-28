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

# Calculate time difference

DateDiff(
    TimeValue(
        Left(
            If(
                Len(Text(ThisItem.ProjectScheduleStartTime)) = 3,
                0 & Text(ThisItem.ProjectScheduleStartTime),
                Text(ThisItem.ProjectScheduleStartTime)
            ),
            2
        ) & ":" & Right(
            If(
                Len(Text(ThisItem.ProjectScheduleStartTime)) = 3,
                0 & Text(ThisItem.ProjectScheduleStartTime),
                Text(ThisItem.ProjectScheduleStartTime)
            ),
            2
        ),
        "en-US"
    ),
    TimeValue(
        Left(
            If(
                Len(Text(ThisItem.ProjectScheduleEndTime)) = 3,
                0 & Text(ThisItem.ProjectScheduleEndTime),
                Text(ThisItem.ProjectScheduleEndTime)
            ),
            2
        ) & ":" & Right(
            If(
                Len(Text(ThisItem.ProjectScheduleEndTime)) = 3,
                0 & Text(ThisItem.ProjectScheduleEndTime),
                Text(ThisItem.ProjectScheduleEndTime)
            ),
            2
        ),
        "EN"
    ),
    Minutes
) / 60 & " Hr"

# Convert Date Int to DateValue

Text(Date(Value(Left(Text(600), 4)), Value(Right(Left(Text(600), 6),2)),Value(Right(Text(600),2))),"dd/mm/yy")

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

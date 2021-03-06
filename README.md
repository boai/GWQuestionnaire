# GWQuestionnaire - easy questionnaires and surveys solution for iOS
-----------------------
![alt tag]( https://raw.github.com/wojczitsu/GWQuestionnaire/master/screenshot.png)

### How to use it 

Creating survey/questionnaire:

    NSMutableArray *questions = [NSMutableArray array];
    
    NSDictionary *a1 = [NSDictionary dictionaryWithObjectsAndKeys:@"YES",@"text",
                                                                [NSNumber numberWithBool:NO],@"marked", nil];
    NSDictionary *a2 = [NSDictionary dictionaryWithObjectsAndKeys:@"NO",@"text",
                                                                [NSNumber numberWithBool:NO],@"marked", nil];
    NSDictionary *a3 = [NSDictionary dictionaryWithObjectsAndKeys:@"A",@"text",
                                                                [NSNumber numberWithBool:NO],@"marked", nil];
    NSDictionary *a4 = [NSDictionary dictionaryWithObjectsAndKeys:@"B",@"text",
                                                                [NSNumber numberWithBool:NO],@"marked", nil];
    NSDictionary *a5 = [NSDictionary dictionaryWithObjectsAndKeys:@"C",@"text",
                                                                [NSNumber numberWithBool:NO],@"marked", nil];
    NSDictionary *a6 = [NSDictionary dictionaryWithObjectsAndKeys:@"1",@"text",     
                                                                [NSNumber numberWithBool:NO],@"marked", nil];
    NSDictionary *a7 = [NSDictionary dictionaryWithObjectsAndKeys:@"2",@"text",
                                                                [NSNumber numberWithBool:NO],@"marked", nil];
    NSDictionary *a8 = [NSDictionary dictionaryWithObjectsAndKeys:@"3",@"text",
                                                                [NSNumber numberWithBool:NO],@"marked", nil];
    NSDictionary *a9 = [NSDictionary dictionaryWithObjectsAndKeys:@"4",@"text",
                                                                [NSNumber numberWithBool:NO],@"marked", nil];
    
    
    // single choice question
    GWQuestionnaireItem *item = [[GWQuestionnaireItem alloc] initWithQuestion:@"Single choice question ?"
                                                        answers:[NSArray arrayWithObjects:a1,a2, nil]
                                                           type:GWQuestionnaireSingleChoice];
    [questions addObject:item];
    
    // multiple choice question
    item = [[GWQuestionnaireItem alloc] initWithQuestion:@"Multiple choice question ?"
                                          answers:[NSArray arrayWithObjects:a3,a4,a5, nil]
                                             type:GWQuestionnaireMultipleChoice];
    [questions addObject:item];
    
    // "Rate" question
    item = [[GWQuestionnaireItem alloc] initWithQuestion:@"Rate it:"
                                          answers:[NSArray arrayWithObjects:a6,a7,a8,a9, nil]
                                             type:GWQuestionnaireRateQuestion];
    [questions addObject:item];
    
    // "open" question
    item = [[GWQuestionnaireItem alloc] initWithQuestion:@"Type your answer:"
                                          answers:nil
                                             type:GWQuestionnaireOpenQuestion];
    [questions addObject:item];
    
    surveyController = [[GWQuestionnaire alloc] initWithItems:questions];
    surveyController.view.frame = CGRectMake(0,20,self.view.frame.size.width,self.view.frame.size.height-20);
    [self.view addSubview:surveyController.view];

Getting results from it:

    // NSLog answers
    for(GWQuestionnaireItem *item in surveyController.surveyItems)
    {
        NSLog(@"-----------------");
        NSLog(@"%@",item.question);
        NSLog(@"-----------------");
        if(item.type == GWQuestionnaireOpenQuestion)
            NSLog(@"Answer: %@", item.userAnswer);
        else
            for(NSDictionary *dict in item.answers)
            {
                NSLog(@"%d - %@",[[dict objectForKey:@"marked"]boolValue], [dict objectForKey:@"text"]);
            }
    }
